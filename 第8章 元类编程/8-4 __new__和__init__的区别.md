## __new__和__init__魔法函数区别
- \_\_new\_\_的功能是在生成对象之前所做的动作, 接受的参数是cls 类
- \_\_init\_\_是在对象生成之后完善对象的属性, 它接受的是self 对象
- 对象生成是在new里面return(返回一个对象)
```
class  User:
    def __new__(cls, *args, **kwargs):
        print("new")
        # return super().__new__(cls) 创建并返回一个类对象

    def __init__(self,name):
        self.name=name
        print("init")

user=User()
>>> new
print(type(user))
>>> <class 'NoneType'>
cls
>>> <class '__main__.User'>
```
在执行user = User时, 首先调用User类中的\_\_new\_\_, 其中cls就是User类, 然后继承父类object的中\_\_new\_\_将创建并返回一个类对象, 然后再执行\_\_init\_\_完善对象属性.









