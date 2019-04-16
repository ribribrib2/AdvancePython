## 序列类型的协议
和容器相关的数据结构的抽象基类都在`from collections import abc`这个模块，我们打开`from _collections_abc import all`，在`_collections_abc.py`模块里面可以看到内容如下：
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
咱们只需要关注“Sequence”, “MutableSequence”, Sequence 是不可变序列类型，MutableSequence 是可变序列类型

## Sequence
### Sequence 继承的类
```
# 继承了两个类 Reversible, Collection
class Sequence(Reversible, Collection):
    # 抽象方法的标识，如果用他必须重写这个方法    
    @abstractmethod            
```
Reversible是序列的翻转，例如ABC变成CBA
```
class Collection(Sized, Iterable, Container):   
    # Sized里面有魔法函数__len__,可以计算序列的长度
    # Iterable是个迭代对象, 有了它可以进行for循环
    # Container里面有魔法函数__contains__，我们就可以用in这个字段，例如 if i in list()   

    __slots__ = ()

    @classmethod
    def __subclasshook__(cls, C):
        if cls is Collection:
            return _check_methods(C,  "__len__", "__iter__", "__contains__")
        return NotImplemented
```
Sequence的所有魔法函数构成了序列的协议,	打开Sequence类我们可以看到里面重写了所继承的抽象基类的方法,包括`__len__`,`__iter__`和`__contains__`.

## MutableSequence
MutableSequence是可变的序列, 他继承了Sequence并新加了一些特性. 如
setitem, delitem, insert, append, clear, reverse, extend, pop, remove, iadd等, 这些都是可变序列的特性.
```
class MutableSequence(Sequence):

    __slots__ = ()

    """All the operations on a read-write sequence.

    Concrete subclasses must provide __new__ or __init__,
    __getitem__, __setitem__, __delitem__, __len__, and insert().

    """

    @abstractmethod
    def __setitem__(self, index, value):
        raise IndexError

    @abstractmethod
    def __delitem__(self, index):
        raise IndexError

    @abstractmethod
    def insert(self, index, value):
        'S.insert(index, value) -- insert value before index'
        raise IndexError
```






