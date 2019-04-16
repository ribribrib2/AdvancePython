## 守护线程、线程阻塞
- setDaemon
- join

## 多线程实例
```
class GetDetailHtml(threading.Thread):
    def __init__(self, name):
        super().__init__(name=name)

    def run(self):
        print("get detail html started")
        time.sleep(2)
        print("get detail html end")

class GetDetailUrl(threading.Thread):
    def __init__(self, name):
        super().__init__(name=name)

    def run(self):
        print("get detail url started")
        time.sleep(4)
        print("get detail url end")

if  __name__ == "__main__":
    thread1 = GetDetailHtml("get_detail_html")
    thread2 = GetDetailUrl("get_detail_url")
    start_time = time.time()
    thread1.start()
    thread2.start()

    # 等待线程执行完才执行主线程
    thread1.join()
    thread2.join()

    #当主线程退出的时候， 子线程kill掉
    print ("last time: {}".format(time.time()-start_time))
```






















