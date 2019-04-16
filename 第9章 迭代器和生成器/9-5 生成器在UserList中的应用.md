## 生成器在List应用
### 生成器是一个迭代器
```
def gen_func():
    yield 1

print(isinstance(gen_func(),Iterator))
>>> True
```

### 查看list的源码
直接dian`a=list`查看list源码发现里面并没有实现方法, 因为list是使用c语言实现的, 但是python中的UserList, 它是python的方式去解释List. 
```
from collections import UserList

class UserList(MutableSequence):
    def __getitem__(self, i): return self.data[i]

class MutableSequence(Sequence):

class Sequence(Reversible, Collection):
    def __iter__(self):
        i = 0
        try:
            while True:
                v = self[i]  # 调用__getitem__
                yield v
                i += 1
        except IndexError:
            return

```
**for循环本质上调用了可迭代对象的`__iter__()`方法，得到了该对象对应的迭代器对象，然后无限调用`__next__()`方法，得到对象中的每一个元素。直到`StopIteration`异常，代表迭代器中已无下一个元素，for循环自动处理该异常，跳出循环。**

- for循环调用list中的`__iter__()`
- 第一次调用`__iter__()`会启动生成器, 执行到yeild, 返回一个生成器对象, v的值保存在生成器对象中.
- for循环拿到值并不断对迭代器调用next, 直到返回异常跳出. 
```
from collections import UserList

class gen_func(UserList):
    def __init__(self, list):
        self.list = list

    def __getitem__(self, item):
        return self.list[item]

    def __iter__(self):
        i = 0
        try:
            while True:
                v = self[i]
                yield v
                i += 1
        except IndexError:
            raise StopIteration

a = gen_func([1,2,3])

for i in a:
    print(i)
```










