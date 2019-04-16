## dict的子类
### UserDict
dict是一个类, 我们就可以尝试继承它:
```
class My_dict(dict):
    def __setitem__(self, key, value):
        super().__setitem__(key,value*value)

a=My_dict(one=2)
print(a["one"])
>>> 2
```
发现值没有变化, 我们去查看dict的源码, 并没有实现`__setitem__`, 这个方法没有做任何处理，并不适用继承:
```
def __setitem__(self, *args, **kwargs): # real signature unknown
    """ Set self[key] to value. """
    pass
```
这个时候我们需要继承UserDict, 它是继承于`MutableMapping`:
```
from collections import UserDict
class My_dict(UserDict):
    def __setitem__(self, key, value):
        super().__setitem__(key,value*value)

a=My_dict(one=2)
print(a["one"])
>>> 4
```
在UserDict的源码中是实现了:
```
def __setitem__(self, key, item): self.data[key] = item
```
所以如果需要继承dict, 我们应该去继承UserDict. 我们可以理解为dict是使用c语言去实现, 而UserDict是使用python语言去实现了一遍dict.

### defaultdict
defaultdict是dict的一个子类, 

我们来看一下`UserDict`中的`__getitem__`的:
```
def __getitem__(self, key):
    if key in self.data:
        return self.data[key]
    if hasattr(self.__class__, "__missing__"):
        return self.__class__.__missing__(self, key)
    raise KeyError(key)
```
如果key不存在就查看有没有`__missing__`, 如果有就调用该方法, 而在`defaultdict`中重载了该方法.
```
def __missing__(self, key): # real signature unknown; restored from __doc__
    """
    __missing__(key) # Called by __getitem__ for missing key; pseudo-code:
        if self.default_factory is None: raise KeyError((key,))
        self[key] = value = self.default_factory()
        return value
    """
    pass
```
使用:
```
from collections import defaultdict

my_dict = defaultdict(dict)
my_value = my_dict["bobby"]
>>> defaultdict(<class 'dict'>, {'bobby': {}})

fruit=["apple","banana","orange"]
v=defaultdict(int)
for i in fruit:
    v[i]+=1
print(v)
>>> defaultdict(<class 'int'>, {'default_factory': 0, 'apple': 1, 'banana': 1, 'orange': 1})
```
