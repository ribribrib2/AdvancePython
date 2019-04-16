## dict
通过抽象基类来理解python中dict的继承关系,
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
dict其实是属于`MutableMapping`, 它继承`Mapping`, `Mapping`继承`Collection`, 里面包括`__len__`,`__iter__`, `__contains__`, 所以dict和序列有很多接近的地方.

a是一个dict对象, 它并不是继承了`MutableMapping`, 而是实现了`MutableMapping`中的方法和魔法函数.
```
from collections.abc import Mapping, MutableMapping
#dict属于mapping类型

a = {}
print (isinstance(a, MutableMapping))
>>> True
```

