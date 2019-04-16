## type的两种用法
- 生成一个类
- 返回一个对象的类型

## type->int->1
- type->class->obj
```
# 1是通过int这个类实例化的对象, int是通过type这个类实例化的对象
>>> a = 1
>>> type(1)
<class 'int'>
>>> type(int)
<class 'type'> 

>>> class Student:
...     pass
...
>>> class MyStudent(Student):
...     pass
...
>>> stu = Student()

>>> type(stu)
<class '__main__.Student'>
>>> type(Student)
<class 'type'>
>>> type(object)
<class 'type'>
>>> type(type)
<class 'type'>

>>> a = 'abc'
>>> type(a)
<class 'str'>
>>> type(str)
<class 'type'> 
>>> type(type)
<class 'type'>

>>> Student.__bases__
(<class 'object'>,)
>>> MyStudent.__bases__
(<class '__main__.Student'>,)
>>> type.__bases__
(<class 'object'>,)
>>> object.__bases__
()
```

## type、object和class的关系
![](http://qiniu.rearib.top/FuGb8QAEGTpbO7AyZtE8VreIHcGF)




