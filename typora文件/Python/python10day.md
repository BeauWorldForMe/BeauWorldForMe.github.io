# 昨日回顾

+ 函数是以功能为导向，减少重复代码、增强可读性。
+ 函数的调用：func()、写几次执行几次
+ 函数的返回值return
  + 终止函数
  + return单个值
  + return多个值，按元组返回
+ 函数的参数：
  + 实参角度：位置参数、关键字参数、混合参数
  + 形参角度：位置参数、默认值参数

# 今日内容

+ 如何在工作中不让别人看出你是培训出来的？

  + 第一天环境安装等等，小白各种问。
  + 项目需求不清晰，也不敢问。
  + 需要学会自主学习，自己解决问题的能力。

+ 形参角度：

  + 万能参数

  ```python
  #万能参数：*args，约定俗成args
  #函数定义时，*代表聚合，将所有的位置参数聚合成一个元组，赋值给agrs这个参数
  def eat(*args):
      print('%s，%s'%args)
  eat('xx','aa')
  
  #练习：
  #使用*args写函数，计算传入函数数字的和。
  def sumnum(*args):
      count=0
      for i in args:
          count += i
      print(count)
  sumnum(1,2,3,4,5)
  
  ```

  ```python
  # **kwargs接收所有关键字参数
  # 函数的定义时： **将所有的关键字参数聚合到一个字典中，将字典赋值给了kwargs
  ```

  + *的魔性用法

    + 在定义时聚合，在函数调用时打散，比如调用时一个参数是一个list类型，会打散list

      ```python
      func(*[1,2,3],*[22,33])
      ```

  + 仅限关键字参数（了解）

    + 形参角度第四个参数，位置应在

      + ```python
        #其中的c就是仅限关键字参数，必须传值，不然报错
        def func(a,b,*args,sex='男',c,**kwargs):
        ```

  + 形参的最终顺序。

    + 位置参数、*args、关键字参数、仅限关键字参数、**kwargs

+ 名称空间：

  + 全局名称空间，局部……

    + 全局：内部变量一个.py文件都能用
    + 局部：临时开辟的空间，内部变量只当前定义的函数内才能用

    ![image-20200620172157475](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200620172157475.png)

    + 内置名称空间：python源码给提供的，比如print等。

  + 加载顺序、取值顺序

    +  1.点击运行，内置名称空间加载到内存
    +  2.全局
    +  3.局部
    + 取值时：就近原则，局部-->全局-->内置，不可逆

  + 作用域

    + 全局作用域：内置名称空间 全局名称空间
    + 局部作用域：局部名称空间

    ```python
    data='周六'
    def func():
        a=666
        print(data)
    print(a)
    #报错：局部作用域可以引用全局作用域，但不能改变。全局作用域不能引用局部的变量，会报错。
    ```

    ![image-20200620175832174](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200620175832174.png)

    ![image-20200620175913794](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200620175913794.png)

    这个图就会报错。因为局部没有新定义count，而改变了全局的count。

    **局部作用域不能改变全局作用域的变量，当python解释器读取到局部作用域时，发现对变量进行的修改操作，解释器会认为你在局部定义了局部变量，而在局部没有找到时，就会报错。**

+ 函数的嵌套（高阶函数）

+ 内置函数globals、locals

  + ```python
    '''
    本文件研究内置函数globals,locals
    '''
    
    a=1
    b=2
    def func():
        name='henri'
        age=23
    print(globals()) #返回一个字典，全局作用域的所有内容
    print(locals())  #返回一个字典，当前作用域的所有内容
    ```

# 今日总结

1. 参数：万能参数，仅限关键字参数，参数的顺序，*的使用：聚合、打散
2. 名称空间，作用域，取值顺序，加载顺序
3. globals、locals
4. 高阶函数：执行顺序
5. **all重点**

# 明天学习

1. 函数名的运用
2. 迭代器

## 代码总行数1637+35=1672行