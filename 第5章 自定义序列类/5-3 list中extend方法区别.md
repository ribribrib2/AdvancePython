## 序列的+、+=和extend的区别
这三个都可以把list进行连接
- 区别一: + 和 +=占用空间不一样

```
a=[1,2,3]
b=[4,5,6]

c=a+b
print(c) # c是产生的新的list

a+=b
print(a) # a还是原来那个list
```

- 区别二: + 两边的数据类型要一致
```
a=[1,2,3]
b=(4,5,6)

a+=b
print(a) # a = [1, 2, 3, 4, 5, 6]

c=a+b

# TypeError: can only concatenate list (not "tuple") to list
print(c) 
```
原因是因为+=是调用`MutableSequence`中的`__iadd__`, 它是调用`extend`, 接收一个`iterable`并通过for循环append.

- entend和append的区别
```
a=[1,2,3]
b=(4,5,6)

a.extend((9,10)) # 利用for循环内的append进行连接
print(a)

a.append(b) # 直接连接的是整体不会拆开合并
print(a)

输出:
    [1, 2, 3, 9, 10]
    [1, 2, 3, 9, 10, (4, 5, 6)]
```






