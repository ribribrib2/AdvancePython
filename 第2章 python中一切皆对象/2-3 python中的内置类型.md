## python中对象的三个特征
### 身份
- 对象在内存中的地址,可以通过id去查看
### 类型
- int类型、字符串类型...
### 值
`a = 1`, 1是指这个对象的值, 1会被python的int类型进行封装, 然后使用a指向1这个对象

## python中的常见内置类型
- None(全局只有一个)
```
a = None
b = None
a和b都是指向同一个对象
```
- 数值
```
int 
float
complex
bool
```
- 迭代类型
- 序列类型
```
list 
bytes、bytearray、memoryview(二进制序列)
range 
tuple 
str 
array
```
- 映射(dict)
- 集合
```
set
frozenset
```
- 上下文管理类型(with)
- 其他
```
模块类型
class和实例函数类型
方法类型
代码类型
object对象
type类型
ellipsis类型
notimplemented类对象
```









 