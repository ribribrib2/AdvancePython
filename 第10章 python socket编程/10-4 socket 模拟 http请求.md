## socket 模拟http请求
- 对url解析得到host和path(调用urllib)
- 使用socket进行连接
- 发送get请求, 然后接受数据
- 对数据进行解析处理
- 最后断开socket连接
```
#requests -> urlib -> socket
import socket
from urllib.parse import urlparse


def get_url(url):
    # 解析url
    url = urlparse(url)
    host = url.netloc
    path = url.path
    if path == "":
        path = "/"

    #建立socket连接
    client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client.connect((host, 80))

    # 发送请求的格式很重要
    client.send("GET {} HTTP/1.1\r\nHost:{}\r\nConnection:close\r\n\r\n".format(path, host).encode("utf8"))

    data = b""
    while True:
        d = client.recv(1024)
        if d:
            data += d
        else:
            break

    data = data.decode("utf8")
    # 去掉request header
    html_data = data.split("\r\n\r\n")[1]
    print(html_data)
    client.close()

if __name__ == "__main__":
    import time
    start_time = time.time()
    for url in range(20):
        url = "http://shop.projectsedu.com/goods/{}/".format(url)
        get_url(url)
    print(time.time()-start_time)

```