## MRO算法
### 为什么不单纯使用深度优先或者广度优先
- 深度优先搜寻

查找顺序是A->B->D->C, 但是如果C重载了D的某个方法(B没有重载该方法), 由于深度优先所以将会使用D中的方法, 这是不合理的

![](http://qiniu.rearib.top/FoNwbOtk2Lb9gNBfQMbTk3SQYP8G)

- 广度优先

查找顺序是A->B->C->D->E, 由于优先级关系, B和D的优先级高于C, 但是如果C和D中定义了同一个方法, 由于广度优先所以将会使用C中的方法, 这是不合理的

![](http://qiniu.rearib.top/Fg5VSJjYJjJRJrVawHIfj8PoawGm)

### C3算法
```
class D:
    pass

class E:
    pass

class C(E):
    pass

class B(D):
    pass

class A(B, C):
    pass

print(A.__mro__)
>>> (<class '__main__.A'>, <class '__main__.B'>, <class '__main__.D'>, <class '__main__.C'>, <class '__main__.E'>, <class 'object'>)
```
```
class D:
    pass

class C(D):
    pass

class B(D):
    pass

class A(B, C):
    pass

print(A.__mro__)
>>> (<class '__main__.A'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.D'>, <class 'object'>)

```


