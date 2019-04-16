## contextlib简化上下文管理器
contextmanager可以简化上下文管理器，不需要我们编写`__enter__`和`__exit__`函数。他给了我们一个机会，让我们把之前一个不是上下文管理器的类变成一个上下文管理器，而不需要我们去修改这个类的源代码. 

其中的yield的作用，是中断当前函数执行流程，先去执行yield出去的部分的代码执行流程

```
import contextlib

@contextlib.contextmanager
def file_open(file_name):
    print ("file open")
    yield 
    print ("file end")

with file_open("bobby.txt") as f_opened:
    print ("file processing")

输出:
    file open
    file processing
    file end
```















