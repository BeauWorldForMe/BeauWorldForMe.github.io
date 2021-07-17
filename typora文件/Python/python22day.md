# 内容回顾

递归练习

sys

os

logging

shutil

函数结束啦

# 今日内容

面向对象

+ 楔子：做一个人狗大战的游戏

  + 技能要有归属感，人是人，狗是狗，技能的函数要写在对应函数内部，闭包。

+ 复杂的，拥有开放式结局的程序 比较适合使用面向对象开发

  + 比如游戏

+ ```python
  #先来定义模子，用来描述一类事物
  #具有相同的属性和动作
  class Person:    #类名
      def __init__(self,name,sex,job,hp,weapon,ad):
          #必须叫这个名字，所有的在一个具体的人物出现之后拥有的属性
          #都可以写在这里
          self.name=name
          self.sex=sex
          self.job=job
          self.level=0
          self.hp=hp
          self.weapon=weapon
          self.ad=ad
          print(self,self.__dict__)
  
  # 类名（）会自动调用其中的__init__方法
  汤达人=Person('汤达人','男','战士',1000,'大剑',220)    # 汤达人 就是对象 这个式子就是类获取对象的过程，实例化
  大胖=Person('大胖','男','弓箭手',700,'弓箭',140)
  二胖=Person('二胖','男','炸弹人',700,'炸弹',200)
  三胖=Person('三胖','女','法师',750,'月火术',160)
  
  汤达人.money=100000   #属性的增加
  print(汤达人.__dict__)
  del 汤达人.money      #属性的删除
  print(汤达人.__dict__)
  ```

+ 实例化所经历的步骤

  + 1.类名()之后的第一个事：开辟一块内存空间
  + 2.调用`__init__`方法，把空间的内存地址作为self参数传递到函数内部
  + 3.所有的这个对象所需要使用的属性，都需要和self关联
  + 4.执行完`__init__`方法中的逻辑后，self变量会自动返回到调用处。

  ```python
  class Dog:    #类名
      def __init__(self,name,hp,kind,ad):
          #必须叫这个名字，所有的在一个具体的人物出现之后拥有的属性
          #都可以写在这里
          self.name=name
          self.hp=hp
          self.kind=kind
          self.ad=ad
          print(self,self.__dict__)
  ```

+ 在类中定义和调用方法

  + 用函数定义的方式即可，参数的第一个位置是self

# 今日总结

面向对象初识

# 明日学习

面向对象的命名空间

## 代码总行数2400+42=2442行