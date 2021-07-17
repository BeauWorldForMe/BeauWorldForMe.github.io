# 昨日回顾

1. 装饰器：完美的呈现了开放封闭原则。本质：闭包。

   ```python
   def wrapper(f):
   	def inner(*args,**kwargs):
           '''在执行被装饰函数之前，想写什么代码写什么代码'''
   		ret=f(*args,**kwargs)
           '''执行被装饰函数之后的操作'''
   		return inner
   	return inner
   ```

2. 练习题

   ```python
   #练习：为函数写一个装饰器，把函数的返回值+100，再返回
   def wrapper(f):
       def inner(*args,**kwargs):
           ret = f(*args, **kwargs)
           return ret+100
       return inner
   
   @wrapper
   def func():
       return 7
   
   result=func()
   print(result)
   ```

   ```python
   #练习：为函数写一个装饰器，一次调用执行五次
   def wrapper(f):
       def inner(*args,**kwargs):
           for i in range(5):
               f(*args, **kwargs)
       return inner
   
   @wrapper
   def func():
       print('in func')
   ```

# 今日内容

1. 自定义模块

   + 什么是模块：一个.py就是一个模块，封装语句的最小单位
   + 不宜过大，便于维护
   + 自定义模块：实际上就是在定义.py文件，其中可以包含：for、if、函数定义等，统称模块的成员

2. 模块的运行方式

   + 脚本方式：直接用解释器执行\pycharm中右键运行
   + 模块方式：被其他的模块导入。为导入它的模块提供资源（函数定义、类定义等）。
   + `'__name__'`的使用
     + 在脚本方式运行时，`'__name__'`是固定的字符串

3. 常用模块:time、datatime、random

4. 系统导入模块的路径

   + 内存中：如果之前成功导入过某个模块，直接引用已经存在的模块。

   + 内置路径中：lib中

   + sys.path:一个路径的列表，没提供源码，c语言写的直接集成到解释器。

     + ```python
       #查看sys.path的内容,并追加a.py
       import sys
       print(sys.path)
       sys.path.append(r'E:\Py Project\day15\a')
       print(sys.path)
       ```

       ```python
       #使用相对位置找到aa文件夹
       #__file__：当前文件的绝对路径
       #使用os模块获取一个路径的父路径
       import os
       print(os.path.dirname(__file__)+'/a') #E:/Py Project/day15/a
       sys.path.append(os.path.dirname(__file__)+'/a')
       ```

     + 三个路径都找不到，就报错

5. `if __name__ == '__main__':`可以快速生成（main+回车）

6. 导入模块的方式

   + import xxx(必须模块名)
   + from xxx import xxx
   + from xxx import *

7. 解决名称冲突的问题

   + 用import xxx导入
   + 自己避免使用同名
   + 使用别名alias，import xxx as aaa（改名成了aaa）

8. 相对导入，两模块在同一个项目里，把一个模块导入另一个。

9. 常用模块random：

   + 此模块提供了和随机数获取相关的方法
     + random.random():获取[0.0,1.0）内浮点数
     + random.randint(a,b):获取[a，b]范围整数
     + random.uniform(a,b):获取[a，b]范围内浮点数
     + random.shuffle(x):把参数指定的数据中的元素打乱
     + random.sample(x,k):从x中取k个数据组成一个列表
     + ……

10. **函数总结**

    + 什么是函数？减少重复性，增强可读性
    + 函数的结构？def 函数名（）：
    + 函数的执行调用：函数名（）
    + 函数的返回值，没有return返回None，返回多个值元组形式。
    + 参数：
      + 形参（位置参数、默认参数、万能参数、仅限关键字参数）
      + 实参（位置参数、关键字参数、混合参数（位置参数一定在前面，一一对应））
      + *的魔性用法：定义聚合、调用打散
    + 空间角度：内置名称空间、全局、局部
    + 作用域：全局作用域、局部作用域
    + 取值顺序和加载顺序
    + 函数的嵌套
    + global：在局部名称空间声明一个全局变量、在局部修改全局变量
    + nonlocal
    + 函数名的应用：指向的就是个内存地址，是个变量
    + 函数的三大器
      + 迭代器
      + 生成器
      + 装饰器：闭包
    + 内置函数

# 今日总结

1. 模块
2. 函数

## 代码总行数1951+91=2042行