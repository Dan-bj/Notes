server.py
```python
import socketserver # 并发的服务端

class FTPServer(socketserver.BaseRequestHandler):    # 必须继承这个类
    def handle(self):    # 必须有这个方法
        while True: # 通信循环
            data = self.request.recv(1024) # self.request就是conn
            self.request.send(data.upper())

if __name__ == '__main__':
    obj = socketserver.ThreadingTCPServer(('127.0.0.1', 9002), FTPServer)
    obj.serve_forever()    # 连接循环
```

client.py
```python
import socket

phone = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
phone.connect(('127.0.0.1', 9002)) # 连接服务器

while True: # 通信循环
    msg = input('>>: ').strip()
    if not msg: continue
    msg_bytes = bytes(msg, encoding='utf-8')
    phone.send(msg_bytes)
    data = phone.recv(1024)
    data_str = str(data, encoding='utf-8')
    print(data_str)
phone.close()
```