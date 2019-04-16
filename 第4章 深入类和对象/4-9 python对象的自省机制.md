## python对象的自省机制
自省是通过一定的机制查询到对象的内部机制, **编程中，自省的能力：检查某些事物以确定它是什么，它知道什么以及它能做什么。**

- \_\_dict\_\_返回的是字典, dir返回的是列表
- \_\_dict\_\_查看对象的所有属性(可写属性), dir查看类本身的所有属性。
```
class Person:
    name = "Person_name"

class Student(Person):
    student_name = 'student_name'
    def __init__(self, school_name):
        self.school_name = school_name

if __name__ == "__main__":
    user = Student("慕课网")

    print(user.__dict__) # 通过__dict__查询属性
    print(user.name)

    # 通过user.name可以读取到, 但是通过__dict__无法获取的原因 
    # name是属于Person的属性, 并不是Student的属性, 但是使用点的时候会向上查找.
    >>> {'school_name': '慕课网'}
    >>> Person_name

    print(Student.__dict__)
    print(Person.__dict__)
    >>> {'__module__': '__main__', 'student_name': 'student_name', '__init__': <function Student.__init__ at 0x00000269CCA83620>, '__doc__': None}
    >>> {'__module__': '__main__', 'name': 'Person_name', '__dict__': <attribute '__dict__' of 'Person' objects>, '__weakref__': <attribute '__weakref__' of 'Person' objects>, '__doc__': None}

    # 通过__dict__赋值
    user.__dict__["school_addr"] = "北京市"
    print(user.school_addr)
    >>> 北京市

    # 通过dir查询属性(只有属性名称)
    print(dir(user))
    print(dir(Student))
    print(dir(Person))
    # 公共部分
    >>> ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', ]
    # 不同部分
    >>> ...'__weakref__', 'name', 'school_name', 'student_name']
    >>> ...'__weakref__', 'name', 'student_name']
    >>> ...'__weakref__', 'name']
```

## __bases__和issubclass
```
class A:
    pass

class B(A):
    pass

class C(B):
    pass

print(C.__bases__)  # (<class '__main__.B'>,)
print(issubclass(C,B)) # True
print(issubclass(C,A)) # True
```