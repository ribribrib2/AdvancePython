## 常用魔法函数(非数学运算类型)
### 字符串表示
- \_\_repr\_\_
- \_\_str\_\_

### 集合序列相关
- \_\_len\_\_
- \_\_getitem\_\_
- \_\_setitem\_\_
- \_\_delitem\_\_
- \_\_contains\_\_

### 迭代相关
- \_\_iter\_\_
- \_\_next\_\_

### 可调用
- \_\_call\_\_

### with上下文管理器
- \_\_enter\_\_
- \_\_exit\_\_

### 数值转换
- \_\_abs\_\_
- \_\_bool\_\_
- \_\_int\_\_
- \_\_float\_\_
- \_\_hash\_\_
- \_\_index\_\_

### 元类相关
- \_\_new\_\_
- \_\_init\_\_

### 属性相关
- \_\_getattr\_\_
- \_\_setattr\_\_
- \_\_getattribute\_\_
- \_\_setattribute\_\_
- \_\_dir\_\_

### 属性描述符
- \_\_get\_\_
- \_\_set\_\_
- \_\_delete\_\_

### 协程
- \_\_await\_\_
- \_\_aiter\_\_
- \_\_anext\_\_
- \_\_aenter\_\_
- \_\_aexit\_\_

## 常用魔法函数(数学运算类型)
### 一元运算符
- \_\_neg\_\_（-）
- \_\_pos\_\_（+）
- \_\_abs\_\_

### 二元运算符
- \_\_lt\_\_(<)
- \_\_le\_\_ <=  
- \_\_eq\_\_ == 
- \_\_ne\_\_ != 
- \_\_gt\_\_ > 
- \_\_ge\_\_ >=

### 算术运算符
- \_\_add\_\_ + 
- \_\_sub\_\_ - 
- \_\_mul\_\_ * 
- \_\_truediv\_\_ / 
- \_\_floordiv\_\_ // 
- \_\_mod\_\_ % 
- \_\_divmod\_\_ 或 divmod() 
- \_\_pow\_\_ 或 ** 或 pow() 
- \_\_round\_\_ 或 round()

### 反向算术运算符
- \_\_radd\_\_ 
- \_\_rsub\_\_ 
- \_\_rmul\_\_ 
- \_\_rtruediv\_\_ 
- \_\_rfloordiv\_\_ 
- \_\_rmod\_\_ 
- \_\_rdivmod\_\_ 
- \_\_rpow\_\_

### 增量赋值算术运算符
- \_\_iadd\_\_ 
- \_\_isub\_\_ 
- \_\_imul\_\_ 
- \_\_itruediv\_\_ 
- \_\_ifloordiv\_\_ 
- \_\_imod\_\_ 
- \_\_ipow\_\_

### 位运算符
- \_\_invert\_\_ ~ 
- \_\_lshift\_\_ << 
- \_\_rshift\_\_ >> 
- \_\_and\_\_ & 
- \_\_or\_\_ | 
- \_\_xor\_\_ ^

### 反向位运算符
- \_\_rlshift\_\_ 
- \_\_rrshift\_\_  
- \_\_rand\_\_ 
- \_\_rxor\_\_ 
- \_\_ror\_\_

### 增量赋值位运算符
- \_\_ilshift\_\_ 
- \_\_irshift\_\_ 
- \_\_iand\_\_ 
- \_\_ixor\_\_
- \_\_ior\_\_


## 调试工具
- notebook

首先使用`pip install -i https://douban.com/simple notebook`安装然后运行`ipython notebook`

## 字符串表示
- \_\_str\_\_

在打印一个实例化对象的时候, python默认会调用str(对象), 对应的魔法函数是\_\_str\_\_
```
class Company(object):
    def __init__(self, employee__list):
        self.employee = employee__list

company = Company(["tom", "bob", "jane"])
print(company)
print(str(company))

<__main__.Company object at 0x000001CFA60BE748>
<__main__.Company object at 0x000001CFA60BE748>
```

- \_\_repr\_\_

\_\_repr\_\_是在开发模式下调用的
```
class Company(object):
    def __init__(self, employee__list):
        self.employee = employee__list

company = Company(["tom", "bob", "jane"])
print(company)
company

<__main__.Company object at 0x0000020A9D7672B0>
<__main__.Company at 0x20a9d7672b0>
```

再次强调, \_\_repr\_\_不是因为该类继承了某一个对象才能去写这个方法, 魔法函数可以写到任何一个定义的类中去, 然后python解释器就是识别出这个对象有该特性, 然后再调试模式下company会被解释器转换为repr(company), 然后再去调用company.\_\_repr\_\_().

```
class Company(object):
    def __init__(self, employee__list):
        self.employee = employee__list

    def __str__(self):
        return ','.join(self.employee)

    def __repr__(self):
        return '.'.join(self.employee)

company = Company(["tom", "bob", "jane"])
print(company) # str 输出
company        # repr输出

tom,bob,jane   # 打印对象
tom.bob.jane   # 调试模式
```











