+ 一个进程包含多个线程
+ 线程可以看做一个子程序

+ 对cpu来说 轮流允许各程序

## 线程的创建

+ 创建一个Thread类或者一个Thread子类的对象

  + 是一个线程类

  + 需要自定义自己的就继承就行

  + ### Thread类

    + java.lang.Thread
    + 常用方法：
      + public void run() 一般需要重写，线程体
      + public void start() 线程启动
      + public static void sleep(long m)线程休眠m毫秒的方法
      + public void join() 优先执行调用join方法的线程

+ 创建一个实现Runnable接口的类的对象

  + 只有一个run方法
  + 是java中用于实现线程的接口
  + 任何实现线程功能的类都必须实现该接口

+ 执行时多线程顺序是随机的

+ start方法只能调用一次，不能多次使用

+ Thread.currentThread()方法

+  .getName()方法，是Runnable接口的方法

+ run当中的代码，可以被多个线程共享

+ ## 线程的状态和生命周期

  + 新建New
  + 可运行Runnable
  + 正在运行Running
  + 阻塞Blocked
  + 终止Dead

![image-20210511215613776](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210511215613776.png)

+ ### sleep()方法使用

  + 作用在指定的毫秒数内让正在执行的线程休眠（ms）
  
  + ```java
    Thread.sleep(1000);
    ```
  
+ ### join()方法使用

  + 作用等待调用该方法的线程结束后才能执行
  + 抢占资源，甚至在主线程前面执行
  + join后面参数可以加毫秒数，是让join让出主动权一次，然后继续join的线程



## 线程优先级

+ MAX_PRIORITY 10

+ MIN_PRIORITY  1

+ NORM_PRIORITY  5

+ 1-10之内

+ 优先级高也不一定一定先执行

+ 使用

  ```
  mt1.setPriority(Thread.MAX_PRIORITY);
  ```

### 各线程争夺CPU的时间来运行，一个正在运行的线程什么时候停是不可控的

+ 如：存取款的项目，存款和取款分开两个线程，可能存款的金额还没完成，数据没更新，就去取款线程了

+ 为了解决这种问题 需要使用synchronized关键字进行同步

+ ### synchronized关键字（线程同步）

  + 用在成员方法、静态方法、语句块

  + ```java
    synchronized(this){
    	//
    }
    ```

+ ### 线程间通信

  + wait()中断方法的执行，使线程等待
  + notify()唤醒处于等待的某一个线程，使其结束等待
  + notifyAll()唤醒处于等待的所有线程，使它们结束等待，一般用这个

