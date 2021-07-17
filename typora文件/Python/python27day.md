# 内容回顾

+ super
  + 遵循mro算法
  + 只在新式类中能适应
  + py2新式类中需要自己添加参数
+ 封装
  + 广义上的封装
  + 狭义上的封装   （__名字）
    + 方法名私有化
    + 实例变量私有化
    + 静态变量私有化
  + 私有化的特点
    + 只能在类的内部使用，不能在外部使用
    + 不能被子类继承
+ 内置函数
  + 装饰器等
  + 反射相关（简化代码）
    + hasattr
    + getattr
    + 字符串数据类型的变量名，getattr(对象，‘变量名’）获取变量的值

# 今日内容

面向对象end

+ 两个装饰器classmethod、staticmethod
+ 一些内置的魔术方法`__new__、__call__、__len__、__eq__、__str__、__repr__、__del__、__enter__、__exit__`



1. classmethod 

   ```python
   #classmethod
   #定义了一个方法，默认传self，但self没被使用，如下：
   class Goods:
       __discount=0.8
       def __init__(self):
           self.__price=5
           self.price=self.__price*self.__discount
       def change_discount(self,new_discount):
           Goods.__discount=new_discount
   apple=Goods()
   print(apple.price)
   #修改折扣0.6
   apple.change_discount(0.6)
   
   apple2=Goods()
   print(apple2.price)
   
   #使用classmethod,程序的修改成本降低了很多，把一个对象绑定的方法，修改为类方法
   class Goods:
       __discount=0.8
       def __init__(self):
           self.__price=5
           self.price=self.__price*self.__discount
       @classmethod
       def change_discount(cls,new_discount):
           cls.__discount=new_discount
   apple=Goods()
   print(apple.price)
   #修改折扣0.6
   apple.change_discount(0.6)
   
   apple2=Goods()
   print(apple2.price)
   ```

   ```python
   #staticmethod 被装饰的方法会成为一个静态方法
   ```

2. 能定义到类中的内容

   + 静态变量：是个所有对象共享的变量
   + 绑定方法：是个自带self参数的函数 由对象调用
   + 类方法：是个自带cls参数的函数 由对象或类调用
   + 静态方法：是个啥都不带的普通函数 由对象或类调用
   + property属性：是个伪装成属性的方法 由对象调用，但不加括号

3. `__call__`方法

   ```python
   #判断callable的对象
   #对象+（）能不能运行，就是callable判断的事
   
   class A:
       def __call__(self, *args, **kwargs):
           print('>>>')
   
   obj=A()
   print(callable(obj))
   obj() #对象+（）就是调用这个类中的__call__方法
   ```

4. `__len__`方法

   ```python
   class Cls:
       def __init__(self,name):
           self.name=name
           self.students=[]
       def __len__(self):
           return len(self.students)
   py22=Cls('py22')
   print(len(py22.students))
   #类中有__len__方法，那这个类的对象就可以使用len()来调用这个方法
   ```

5. `__new__`方法

   ```python
   #__new__
   class A:
       def __init__(self):
           print('init')
       def __new__(cls, *args, **kwargs):
           print('new')
           return super().__new__(cls)
   A()
   '''
   new
   init
   '''
   ```

   new来开空间，借用父类object的new，不用自己写，在类中先调用new，在调用init

6. 设计模式--单例模式

   + 一个类 从头到尾 只会创建一次self空间
   + 如果在模块中写，每次导入都是单例
   + 网络编程的时候会再提到

7. `__str__``__retr__`方法

8. 选课系统的需求分析

   + 功能概述：学生选课
   + 需求分析：
     + 核心功能：**选课**
   + 角色：学生、管理员
   + 工作流程：
     + 登录：用户名密码
     + 判断身份：在登陆的时候判断是学生还是管理员
     + 学生用户：登录之后三个功能
       + 1.查看所有课程
       + 2.选择课程
       + 3.查看所选课程
       + 4.退出程序
     + 管理员用户:
       + 创建课程
       + 创建学生账号
       + 查看所有课程
       + 查看所有学生
       + 查看学生选课情况
       + 退出程序
     + 课程：
       + 属性：课程名、价格、周期、老师
     + 学生：
       + 属性：姓名，所选课程
       + 方法：查看可选课程、选择课程、查看所选课程、退出
     + 管理员
       + 属性：姓名
       + 方法：创建课程、创建学生账号、查看所有课程、查看所有学生、查看选课情况、退出

   ![image-20200707133440201](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200707133440201.png)

   

# 

## 代码总行数2764+59=2823行