IO multiplexing这个词可能有点陌生，但是如果我说select，epoll，大概就都能明白了。有些地方也称这种IO方式为event driven IO。我们都知道，select/epoll的好处就在于单个process就可以同时处理多个网络连接的IO。它的基本原理就是select/epoll这个function会不断的轮询所负责的所有socket，当某个socket有数据到达了，就通知用户进程。它的流程如图：

![](./img/5-3.gif)

当用户进程调用了select，那么整个进程会被block，而同时，kernel会“监视”所有select负责的socket，当任何一个socket中的数据准备好了，select就会返回。这个时候用户进程再调用read操作，将数据从kernel拷贝到用户进程。

这个图和blocking IO的图其实并没有太大的不同，事实上，还更差一些。因为这里需要使用两个system call (select 和 recvfrom)，而blocking IO只调用了一个system call (recvfrom)。但是，用select的优势在于它可以同时处理多个connection。（多说一句。所以，如果处理的连接数不是很高的话，使用select/epoll的web server不一定比使用multi-threading + blocking IO的web server性能更好，可能延迟还更大。select/epoll的优势并不是对于单个连接能处理得更快，而是在于能处理更多的连接。）

在IO multiplexing Model中，实际中，对于每一个socket，一般都设置成为non-blocking，但是，如上图所示，整个用户的process其实是一直被block的。只不过process是被select这个函数block，而不是被socket IO给block。

*结论: select的优势在于可以处理多个连接，不适用于单个连接*

sever.py
```python
import socket
import select
sk = socket.socket()
sk.bind(("127.0.0.1",8800))
sk.listen(5)
sk.setblocking(False)
inputs = [sk, ]

while True:
    r, w, e = select.select(inputs, [], [], 5)  # 可以监听端口是否有人连接还可以监听连接后的对象有没有变化
    print(len(r))

    for obj in r:
        if obj == sk:
            conn, add = obj.accept()
            print("conn:", conn)
            inputs.append(conn)
        else:

            data_byte = obj.recv(1024)
            print(str(data_byte, 'utf8'))
            if not data_byte:
                inputs.remove(obj)
                continue
            inp = input('回答%s: >>>' % inputs.index(obj))
            obj.sendall(bytes(inp, 'utf8'))

    print('>>', r)
```

client.py
```python
import socket
sk = socket.socket()
sk.connect(('127.0.0.1', 8802))

while True:
    inp = input(">>>>")   # how much one night?
    sk.sendall(bytes(inp, "utf8"))
    data = sk.recv(1024)
    print(str(data, 'utf8'))
```

思考1：select监听fd变化的过程
用户进程创建socket对象，拷贝监听的fd到内核空间，每一个fd会对应一张系统文件表，内核空间的fd响应到数据后，就会发送信号给用户进程数据已到；用户进程再发送系统调用，比如（accept）将内核空间的数据copy到用户空间，同时作为接受数据端内核空间的数据清除，这样重新监听时fd再有新的数据又可以响应到了（发送端因为基于TCP协议所以需要收到应答后才会清除）。

思考2: 上面的示例中，开启三个客户端，分别连续向server端发送一个内容（中间server端不回应），结果会怎样，为什么？























