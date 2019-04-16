## dict的常用操作
- clear

clear的功能是对dict的内容进行清除.没有任何的返回值
```
a={"person1":{"Andy":30},"person12":{"Lady":45}}
a.clear()
print(a)
>>> {}
```

- 浅copy和深copy

- fromkeys

首先这是一个静态方法, 可以直接使用类名调用
```
@staticmethod # known case
def fromkeys(*args, **kwargs): # real signature unknown
    """ Returns a new dict with keys from iterable and values equal to value. """
    pass
```
```
a=["person1","person2"]

b=dict.fromkeys(a,"company")
print(b)
>>> {'person1': 'company', 'person2': 'company'}
```

- get

解决key没有对应的value报错的问题
```
print(a.get("person",{}))
```

- items, keys, values

取值

- pop，popitem

删除并返回

- setdefault

如果key存在使用get方法, 如果key不存在使用set方法

- update

两个字典合并
```
a={"person1":{"Andy":30},"person12":{"Lady":45}}
b={"person1":{"Andy":40},"person20":{"Lady":80}}
print(b.update(a)) # 没有返回值
>>> None
print(b) # 如果key重复, 使用a的value
>>> {'person1': {'Andy': 30}, 'person20': {'Lady': 80}, 'person12': {'Lady': 45}}
```
