## 抽象基类
- 抽象基类是一个虚拟的类, 相当于一个模板, 定义一些方法, 所有继承这个基类的类必须覆盖抽象基类里面的方法
- 抽象基类是无法用来实例化的

### 为什么要有抽象基类
因为python是基于鸭子类型的, 所以其实只要实现某些方法就可以了, 那为什么还要抽象基类呢?
- 第一种用法:我们去检查某个类是否有某一种方法

某些情况之下希望判定某个对象的类型, 可以使用`hasattr`判断是否实现某方法或者使用`isinstance`(推荐)去判断一个类是否是指定的类型, `Sized`就是一个实现`__len__`的抽象基类.
```
class Company(object):
    def __init__(self, employee_list):
        self.employee = employee_list

    def __len__(self):
        return len(self.employee)

com = Company(["bobby1","bobby2"])
print(hasattr(com, "__len__"))

from collections.abc import Sized
print(isinstance(com, Sized))
>>> True

# Sized内部的类方法, 在调用isinstance(com, Sized)时cls就是Sized对象, C就是com对象,然后判断com对象有没有实现__len__方法.
@classmethod
def __subclasshook__(cls, C):
    if cls is Sized:
        return _check_methods(C, "__len__")
    return NotImplemented

# isinstance还会找到继承链去进行判断
class A:
    pass

class B(A):
    pass

b = B()
print(isinstance(b, A))
>>> True
```
- 第二种用法: 强制某个子类必须实现某些方法
```
# 模拟抽象基类, 只有在调用set方法的时候才会抛出异常
class CacheBase():
    def get(self, key):
        raise NotImplementedError
    def set(self, key, value):
        raise NotImplementedError

class RedisCache(CacheBase):
    def set(self, key, value):
        pass

redis_cache = RedisCache()
redis_cache.set("key", "value")

# 使用abc模块, 在初始化的时候就会去判断有没有重载基类的方法,没有就抛异常
import abc

class CacheBase(metaclass=abc.ABCMeta):
    @abc.abstractmethod
    def get(self, key):
        pass

    @abc.abstractmethod
    def set(self, key, value):
        pass

class RedisCache(CacheBase):
    def set(self, key, value):
        pass
    def get(self, key):
        pass

redis_cache = RedisCache()
```

### collection.abc模块
在这个模块中定义了很多通用的抽象基类, 比如Sized. 但是这些抽象基类定义出来并不是用来继承的, 更多的是让我们理解接口的一些定义. 推荐使用鸭子类型或者多继承(Mixin)实现, 而少用抽象基类.
```
__all__ = ["Awaitable", "Coroutine",
           "AsyncIterable", "AsyncIterator", "AsyncGenerator",
           "Hashable", "Iterable", "Iterator", "Generator", "Reversible",
           "Sized", "Container", "Callable", "Collection",
           "Set", "MutableSet",
           "Mapping", "MutableMapping",
           "MappingView", "KeysView", "ItemsView", "ValuesView",
           "Sequence", "MutableSequence",
           "ByteString",
           ]
```

### 声明抽象基类
- metaclass = abc.ABCMeta
- @abc.abstractmethod

