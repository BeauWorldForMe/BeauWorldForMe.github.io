# 内容回顾

概念

+ 同步异步阻塞和非阻塞

  + 同步阻塞：调用一个函数需要等待这个函数的执行结果，并且在执行这个函数的过程中CPU不工作

    + ```python
      inp=input('>>>')
      ```

  + 同步非阻塞：调用一个函数需要等待这个函数的执行结果，在执行这个函数的过程中CPU工作

    + ```python
      ret=eval('1+2+3-4')
      ```

  + 异步非阻塞：调用一个函数不需要等待这个函数的执行结果，并且在执行这个函数的过程中CPU工作

    + ```python
      start()
      ```

  + 异步阻塞：调用一个函数不需要等待这个函数的执行结果，在执行这个函数的过程中CPU不工作

    + ```python
      #开启十个进程 异步的
      #获取这个进程的返回值，并且能做到哪一个进程先结束，就先获取谁的返回值。
      ```

+ 进程的三状态图

  + 就绪 ----->操作系统调度 ---->运行 ----->遇到io操作 ----> 阻塞
  + ​                                                         ----->时间片到了 ----> 就绪

+ 进程和调度算法：短作业和长作业是有区别的，越长的作业被调度的没有短作业积极，每个io操作都会让你辛苦排队得来的执行CPU机会让给其他程序

  + 先来先服务
  + 短作业优先
  + 分时的概念
  + 多级反馈算法

+ 进程开启和关闭

  + 父进程 开启了 子进程
  + 父进程 要负责给 子进程 回收子进程结束后的资源

# 今日内容

Process类拾遗

+ 开启进程的另一种方法

  ```python
  from multiprocessing import Process
  import os
  import time
  
  class MyProcess(Process):
      def __init__(self,a,b,c):
          self.a=a
          self.b=b
          self.c=c
          super().__init__()
      def run(self):
          time.sleep(1)
          print(os.getppid(),os.getpid(),self.a,self.b,self.c)
  
  if __name__ == '__main__':
      print('----->',os.getpid())
      for i in range(10):
          p=MyProcess(1,2,3)
          p.start()
          print(p.pid,p.ident)
          print(p.name)
          print(p.is_alive())
          p.terminate() #强制结束一个子进程
          print(p.is_alive())
          time.sleep(0.01)
          print(p.is_alive())
  ```

+ Process类的一些其他方法和属性

  + name pid daemon

+ 守护进程

  ```python
  import time
  from multiprocessing import Process
  
  def son1():
      while True:
          print('in son1')
          time.sleep(1)
  
  def son2():
      for i in range(10):
          print('in son2')
          time.sleep(1)
  
  if __name__ == '__main__':
      p1=Process(target=son1)
      p1.daemon=True  # 表示设置p1是一个守护进程
      p1.start()
      p2=Process(target=son2).start()
      time.sleep(5)
      print('in main')
  # 主进程会等待所有的子进程结束，是为了回收子进程的资源
  # 守护进程会等待主进程的代码执行结束后再结束，而不是等待整个主进程
  # 守护进程结束和其他子进程的结束与否无关
  ```

进程同步---lock锁

+ 抢票的时候，有人买了，票就会立刻少

进程之间通信--队列

+ 生产者消费者模式
  + 爬虫的时候
  + 分布式操作：celery
  + 本质：就是让生产数据和消费数据的效率达到平衡并最大化
  + consumer producer

进程之间的数据共享----Manager

## 代码总行数3047+49=3096行

