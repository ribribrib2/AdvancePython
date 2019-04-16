## 全局解释器锁
GIL的全称是Global Interpreter Lock, 
- python中一个线程对应于c语言中的一个线程
- GIL使得同一个时刻只有一个线程在一个cpu上执行字节码, 无法将多个线程映射到多个cpu上执行
- GIL会根据执行的字节码行数以及时间片释放gil, gil在遇到io的操作时候主动释放

## GIL的特点：
- Python在多线程下，每个线程的执行方式为：
1. 获取GIL
2. 执行代码直到sleep或者是python虚拟机将其挂起。
3. 释放GIL

一个CPU只能执行一个线程, 例如一个CPU 有三个线程, 首先线程A执行, 然后线程A达到释放条件进行释放GIL, 线程B和线程C进行竞争GIL, 谁抢到GIL, 继续执行.

## GIL无法保证线程绝对安全
```
total = 0

def add():
    global total
    for i in range(1000000):
        total += 1
def desc():
    global total
    for i in range(1000000):
        total -= 1

import threading
thread1 = threading.Thread(target=add)
thread2 = threading.Thread(target=desc)
thread1.start()
thread2.start()

thread1.join()
thread2.join()
print(total)
```


