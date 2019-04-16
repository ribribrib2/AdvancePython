## 使用多线程实现多用户连接
```
import socket
import threading

server = socket.socket()
server.bind(('0.0.0.0', 8000))
server.listen()

# 可以添加收到某个指令break出where循环然后close连接
def handler_sock(conn, addr):
    while True:
        data = conn.recv(1024)
        print(data.decode('utf-8'))
        input_data = input()
        conn.send(input_data.encode('utf-8'))


while True:
    conn, addr = server.accept()
    client_thread = threading.Thread(target=handler_sock, args=(conn, addr))
    client_thread.start()
```

```
import socket

server = socket.socket()
server.connect(('127.0.0.1', 8000))
while True:
    input_data = input()
    server.send(input_data.encode('utf-8'))
    data = server.recv(1024)
    print(data.decode('utf-8'))
```
















