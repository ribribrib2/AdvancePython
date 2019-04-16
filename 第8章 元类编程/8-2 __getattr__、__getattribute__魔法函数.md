## __getattr__和__getattribute__的区别
### \_\_getattr__
当实例化对象调用属性不存在的时候调用
```
class A:
    def __init__(self):
        pass

a=A()
print(a.age)
>>> AttributeError: 'A' object has no attribute 'age'
```
```
class A:
    def __init__(self):
        pass
    def __getattr__(self, item):
        print("即使你没有属性也不会报错")

a=A()
print(a.age)
>>> 即使你没有属性也不会报错
>>> None
```
作用: 我们可以指定在找不到该属性的时候实现的操作, 比如修改查找的名称, 重新指定查找的区域等

### \_\_getattribute__
执行查找, 无条件进入该魔法函数, 即使所查找的属性不存在






















