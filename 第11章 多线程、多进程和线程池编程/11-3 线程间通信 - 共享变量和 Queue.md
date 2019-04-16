## 数据共享
- 共享变量

使用一个全局变量, 然后不同线程可以访问并修改这个变量

- queue
```
from queue import Queue

detail_url_queue = Queue(maxsize=1000)

queue.put("http://projectsedu.com/{id}".format(id=i))
url = queue.get()
```

















