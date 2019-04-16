## set 和 frozenset的应用场景及区别
- set是集合，frozenset是不可变集合。
- set最大的特性是不重合，在去重的时候用的最多。
- set是无序的
- set的性能比较高, 因为他用到了哈希编码
```
def __init__(self, seq=()): # known special case of set.__init__
    """
    set() -> new empty set object
    set(iterable) -> new set object
    
    Build an unordered collection of unique elements.
    # (copied from class doc)
    """
    pass
```
set初始化是接收一个可迭代对象, 比如str, list, dict, tuple...

set的另一种初始化方式是{'a','b','c'}

### frozenset
不可变集合是无法修改的, 可以作为dict的key
```
a={"a","b","c"}
a.add("d") # 正常

a=frozenset("abcd")
a.add("d") # 报错
```

### 常用方法
- update 方法
```
a=set("abc")
a.update("bcd") # 取的是总集
print(a)
>>> {'b', 'd', 'a', 'c'}
```
- 集合运算(|，&，-)
```
a=set("abc")
b=set("bcd")
print(a - b) # 对a进行去重
print(a | b) # 并集
print(a & b) # 交集

{'a'}
{'c', 'b', 'd', 'a'}
{'c', 'b'}
```
原理是调用了相应的魔法函数











