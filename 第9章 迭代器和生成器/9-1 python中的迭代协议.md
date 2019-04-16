## 什么是迭代协议
### 迭代器是什么？ 
- 迭代器是访问集合内元素的一种方式，一般用来遍历数据
- 迭代器和以下标的访问方式不一样，迭代器是不能后退的, 迭代器提供了一种惰性方式数据的方式
- list可以先取第1个然后再取第0个, 但是迭代器不可以.
- 可迭代对象必须实现`__iter__`, 迭代器必须实现`__iter__`和`__next__`
- list中有`__iter__`, 是一个可迭代对象, 但不是迭代器
- 可迭代对象调用`iter(a)`返回一个迭代器

### for循环
在调用for循环的时候会尝试调用`iter()`, 然后`iter()`首先会去找有没有`__iter__`, 如果有将返回一个迭代器, 如果没有将查看有没有`__getitem__`, 如果有将创建默认的迭代器使用`__getitem__`进行迭代输出.

### 自己实现一个迭代器和可迭代对象
把迭代器和可迭代对象分开, 把维护取值放在迭代器中
```
from collections.abc import Iterator

class Company(object):
    def __init__(self, employee_list):
        self.employee = employee_list

    # 可迭代对象中的__iter__返回迭代器
    def __iter__(self):
        return MyIterator(self.employee)

class MyIterator(Iterator):
    def __init__(self, employee_list):
        self.iter_list = employee_list
        self.index = 0 # 需要在内部维护一个取值位置

    # 继承了Iterator可以不写该方法, 如果重写那么return self
    # def __iter__(self):
    #     return self

    def __next__(self):
        #真正返回迭代值的逻辑
        try:
            word = self.iter_list[self.index]
        except IndexError:
            raise StopIteration # 抛出的异常应该是StopIteration
        self.index += 1
        return word
```






