## 效率
- dict查找的性能远远大于list
- 在list中查找元素时间会随着list的增大而增大
- 在dict中查找元素时间不会随着dict的增大而增大

- 哈希表

![](http://qiniu.rearib.top/FkAaL7P2cDUdEPyd812DzGZLAGMC)

- 哈希表查找

![](http://qiniu.rearib.top/FgfZpFaH8FB0mtw5sHchevL0TrUA)


1. dict的key或者set的值都必须是可以hash的
2. 不可变对象都是可hash的, str,fronzenset,tuple
3. 自己实现的类使用魔法函数`__hash__`实现哈希
4. dict的内存花销大，但是查询速度快，自定义的对象或者python内部的对象都是用dict包装的
5. dict的存储顺序和元素添加顺序有关
6. 添加数据有可能改变已有数据的顺序, 最开始会申请内存, 然后随着数据的不断添加, 当剩余空间小于三分之一的时候会申请新的内存然后进行数据迁移, 这个时候存储顺序可能会发生改变.