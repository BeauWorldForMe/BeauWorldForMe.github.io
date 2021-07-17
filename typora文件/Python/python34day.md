# 内容回顾

+ 开启进程的另一种方式

  + ```python
    form multiprocessing import Process
    class 类名(Process):
    	def __init__(self):
    	...
    	
    p=类名()
    p.start()
    ```

+ 守护进程

  + ```python
    p=类名()
    p.daemon=True #设置守护进程
    p.start()
    #一般情况下多个进程的执行顺序，可能是
    #主进程代码结束，守护进程结束，子进程结束，主进程结束
    #子进程结束，主进程代码结束，守护进程结束，主进程结束
    ```

+ 锁

  + 

+ 队列

+ 生产者消费者模型

# 今日内容

+ 进程的内容
  + 生产者消费者模型
    + 爬取网页
  + 数据共享
    + Manager类
+ 线程的概念
+ python当中的线程的特点
+ threading模块开启线程
+ ftp作业需求分析

## 代码总行数3096行