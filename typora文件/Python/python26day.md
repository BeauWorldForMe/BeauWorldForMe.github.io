# 内容回顾

多态：

​	一个类表现出的多种形态，实际上是通过继承来完成的

# 今日内容

1. super，调用父类的同名方法

   按照mro顺序来寻找当前类的下一个类

2. 封装

   + 广义上的封装

     + 方法属性名字前加了__，就变成了私有的，所有私有的内容或名字都不能在类的外部调用，只能在内部使用

   + 狭义上的封装

     + 封装的语法
       + 私有的静态变量
       + 私有的实例变量
       + 私有的绑定方法

   + 所有的私有化都是为了让用户不在外部调用类中的某个名字

   + 如果完成私有化 那么这个类的封装度就更高了 封装度越高各种属性的安全性就越高，但代码复杂

   + 加了双下划线为什么不能从类的外部调用了？

     + ```python
       class User:
           __Country='China'
           __Role='法师'
       print(User._User__Country)#这样也能找到
       ```

       没有绝对的数据安全，定义的双下划线内容，其实存储时自动完成变形，变成了_类名__方法

   + 私有的内容能不能被子类使用呢？

     + 否

   + 私有的原理：变形

3. 在其它语言中的数据级别都有哪些?在python中有哪些？

   + public 公有的，类内类外都能用，父类子类都能用
   + protect 保护的，类内能用，父类子类都能用，类外不能用
   + private 私有的，类内能用，本类能用，其他地方都不行

4. 类中的三个装饰器（内置函数）

   + property

     ```python
     #property I
     #
     from math import pi
     class Circle:
         def __init__(self,r):
             self.r=r
         def area(self):
             return pi*self.r**2
     
     c1=Circle(5)
     print(c1.r)
     print(c1.area())
     
     ##
     from math import pi
     class Circle:
         def __init__(self,r):
             self.r=r
         @property #把一个方法伪装成属性，在调用这个方法时不需要加括号就能用，装饰的这个方法不能有参数
         def area(self):
             return pi*self.r**2
     
     c1=Circle(5)
     print(c1.r)
     print(c1.area)
     ```

     ```python
     #property的第二个应用场景:和私有属性合作
     class User:
         def __init__(self,usr,pwd):
             self.usr=usr
             self.__pwd=pwd
         @property
         def pwd(self):
             return self.__pwd
     
     汤达人=User('汤达人','123')
     print(汤达人.pwd)
     ```

     + setter（了解）
     + delter（了解）

   + classmethod

   + staticmethod

5. 反射

   + 概念：用字符串数据类型的名字，来操作这个名字对应的函数、实例变量、绑定方法...

   + ```python
     name='henri'
     age=22
     n=input('>>>')
     if n=='name':
         print(name)
     elif n=='age':
         print(age)
     #这样变量多了很麻烦
     #有些时候明明知道一个变量的字符串数据类型的名字，但调不到，用反射
     ```

   + 反射对象的 实例变量

   + 反射类的 静态变量、绑定方法

   + 模块中的 所有变量

     + 被导入的模块
     + 当前执行的py文件--脚本

   + ```python
     class Person:
         def __init__(self,name,age):
             self.name=name
             self.age=age
     
     henri=Person('henri',22)
     leo=Person('leo',23)
     
     ret=getattr(henri,'name')
     print(ret)
     ret=getattr(leo,'name')
     print(ret)
     #这就是反射
     ```



## 代码总行数2702+62=2764行