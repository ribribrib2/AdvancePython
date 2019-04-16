## 上下文管理器
### 异常捕捉中的return
```
def exe_try():
    try:
        print ("code started")
        raise KeyError
        return 1 # 不会被执行
    except KeyError as e:
        print ("key error")
        return 2 # 压入堆栈
    else:
        print ("no error")
        return 3
    finally:
        print ("finally")
        return 4 # 压入堆栈, 最后取出栈顶

print(exe_try())

输出:
    code started
    key error
    finally
    4  # 不是输出2, 而是4
```

## 上下文管理器协议
with语句后面的as得到的是是__enter__方法的返回值, 如果`__enter__`返回1, 那么sample就等于1. 
```
class Sample:
    def __enter__(self):
        # 获取资源
        print ("enter")
        return self
    def __exit__(self, exc_type, exc_val, exc_tb):
        #释放资源
        print ("exit")
    def do_something(self):
        print ("doing something")

with Sample() as sample:
    sample.do_something()

输出:
    enter
    doing something
    exit
```

如果`__enter__`没有返回值, 那么无法使用as.
```
class Person:
    def __enter__(self):  # 获取资源
        print("enter")

    def __exit__(self, exc_type, exc_val, exc_tb):  # 释放资源
        print("exit")

    def said(self):
        print("said")


with Person() as P:
    P.said()

>>> AttributeError: 'NoneType' object has no attribute 'said'
```



















