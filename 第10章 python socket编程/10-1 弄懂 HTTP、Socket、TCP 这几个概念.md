## 基本概念
- 推荐书籍: TCP/IP详解 卷1: 协议

### 五层网络模型
![](http://qiniu.rearib.top/Fr5eDJbpDM45IXmPajqNFUceyFoV)

操作系统给我们提供了一个socket接口, 用于实现TCP和UDP, 它不属于任何协议

### socket编程
![](http://qiniu.rearib.top/Fnpjj9hCnNMMCuVol3aoKsUgZgiB)

django的socket是存在于uwsgi中

### 数据格式转换
```
import socket, json 

server = socket.socket()
server.bind(('0.0.0.0', 8000))
server.listen()

a = {'1': 1, '2': 2, '3': 3}

while True:
    # 如果没有新的链接过来会堵塞在这里
    conn, addr = server.accept()
    data = conn.recv(1024)
    # 接收的数据是bytes类型, 需要解码成unicode字符串
    print(data.decode('utf-8'))
    # 首先对字典进行序列化, 从对象变成字符串, 然后再转换成bytes类型
    conn.send(json.dumps(a).encode('utf-8'))
    conn.close()


import socket
import json

server = socket.socket()
server.connect(('127.0.0.1', 8000))
server.send('456'.encode('utf-8'))
data = server.recv(1024)
# 接收的data是bytes类型
print(json.loads(data))
>>> {'1': 1, '2': 2, '3': 3}
print(json.loads(data.decode('utf-8')))
>>> dict对象输出
server.close()
```







