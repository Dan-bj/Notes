### server.py
```python
import socket, subprocess, struct, json

phone = socket.socket(socket.AF_INET, socket.SOCK_STREAM) # AF_INET基于网络通信，SOCK_STREAM基于TCP
phone.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1) # 地址重用
phone.bind(('127.0.0.1', 9999)) # 绑定IP和端口
phone.listen(5) # 开始监听

while True: # 连接循环
    conn, addr = phone.accept() # 等待连接
    print('客户端地址', addr)
    while True: # 通信循环
        try:
            cmd_bytes = conn.recv(1024) # 收数据
            cmd_str = str(cmd_bytes, encoding='utf-8')
            print('command: ', cmd_str)
            if not cmd_bytes: break
            res = subprocess.Popen(cmd_str, shell=True, stderr=subprocess.PIPE, stdout=subprocess.PIPE) # 执行命令
            res_stdout = res.stdout.read() # 获取命令执行的结果
            res_stderr = res.stderr.read()
            data_size = len(res_stdout) + len(res_stderr)
            head_dic = {'data_size': data_size} # 定义报头
            head_json = json.dumps(head_dic)
            head_bytes = bytes(head_json, encoding='utf-8')
            head_len = len(head_bytes)
            conn.send(struct.pack('i', head_len)) # 发送包头长度
            conn.send(head_bytes) # 发送报头
            conn.send(res_stderr) # 发送数据
            conn.send(res_stdout)
        except Exception as e:
            print(e)
            break

    conn.close() # 关闭连接

phone.close() # 关闭监听
```

### client.py
```python
import socket, struct, json

phone = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
phone.connect(('127.0.0.1', 9999)) # 连接服务器

while True: # 通信循环
    cmd = input('>>: ').strip()
    if not cmd: continue
    phone.send(cmd.encode('utf-8')) # 发送数据必须是bytes格式
    head_len_struct = phone.recv(4) # 收报头长度
    head_len = struct.unpack('i', head_len_struct)[0]
    head_bytes = phone.recv(head_len) # 收报头
    head_json = str(head_bytes, encoding='utf-8')
    head_dic = json.loads(head_json)
    data_size = head_dic['data_size'] # 解包

    data_all = b''
    while data_size > 0:
        data = phone.recv(1024)
        data_all += data
        data_size -= len(data)

    data_str = str(data_all, encoding='utf-8')
    print(data_str)
phone.close()
```

