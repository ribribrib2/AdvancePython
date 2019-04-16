## python中函数的工作原理
```
def foo():
    bar()
def bar():
    pass
foo()
```
- python的解释器会用`PyEval_EvalFramEx(C语言)`函数去执行我们的foo函数.
- 在运行foo函数的时候首先会创建一个栈帧(Stack frame), 这个栈帧是一个上下文, 也是一个对象.
- 栈帧会将foo函数变成一个字节码对象, 使用dis查看字节码
- 然后栈帧的上下文中去运行字节码(字节码是全局唯一的)
```
def foo():
    bar()
def bar():
    pass

import dis
print(dis.dis(foo))

2           0 LOAD_GLOBAL              0 (bar)
            2 CALL_FUNCTION            0
            4 POP_TOP
            6 LOAD_CONST               0 (None)
            8 RETURN_VALUE
None
```
- 当foo调用bar, 又会创建一个新的栈帧, 然后运行bar的字节码
- 所有的栈帧都是分配在堆的内存上, 如果不释放会一直存在, 所以栈帧可以独立于调用者存在, 就比如调用者foo不存在也没关系, 只要指针指向bar的栈帧就可以控制
```
import inspect
frame = None
def foo():
    bar()
def bar():
    pass
    global frame
    # 获取当前函数的栈帧并赋给全局变量frame
    frame = inspect.currentframe()

foo()
print(frame.f_code.co_name)
>>> bar
caller_frame = frame.f_back
print(caller_frame.f_code.co_name)
>>> foo
```

![](http://qiniu.rearib.top/FiCM74pMYvC5Xz3gPHcSVLs5SFZt)

- python解释器会编译字节码, 如果发现有yeild, 就会标记该函数, 然后再调用的时候会返回一个生成器对象. 而这个生成器对象实际上是把这个frame对象做了一个封装

![](http://qiniu.rearib.top/FvNYTPLMxcqeAfZruBN-2CoaHOKV)

- 生成器可以在任何时候、任何函数中恢复运行，因为它的栈帧并不在真正的栈中，而是堆中
- f_lasti指向“最后执行指令”的指针。初始化为 -1，意味着它没开始运行















