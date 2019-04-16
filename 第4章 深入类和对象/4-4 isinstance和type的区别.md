## type与isinstance区别：
1. type用于求一个未知数据类型的对象，isinstance用于判断一个对象是否是已知类型；
2. type不认为子类是父类的一种类型，isinstance认为子类是父类的一种类型，即子类对象也属于父类类型.
```
class A:
    pass

class B(A):
    pass

b = B()

# instance用于判断一个对象是否是已知类型
print(isinstance(b, B)) # True
print(isinstance(b, A)) # True isinstance会根据继承链去判断

# 求一个未知数据类型的对象
print(type(b)) # <class '__main__.B'>

# type不认为子类是父类的一种类型，isinstance认为子类是父类的一种类型，即子类对象也属于父类类型.

# is是去判断这两个是不是一个对象, 即id是否相同
# ==是判断值是否相等
print(type(b) is B) # True 得到的是B的地址
print(type(b) is A) # False

print(id(B)) # 1943999460392
print(id(type(b))) # 1943999460392
print(B) # <class '__main__.B'>

a=[1,2,3]
b=[1,2,3]
c=a

print(id(a)) # 2065494827720
print(id(b)) # 2065493557192
print(id(c)) # 2065494827720

print(a is b) # False
print(c is a) # True
print((a==b)) # True 
```