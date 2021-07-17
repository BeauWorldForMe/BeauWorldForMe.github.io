# 内容回顾

+ 命名空间
+ 组合
  + 一个类的对象是另一个类对象的属性
  + 两个类之间有 什么有什么二点关系：例：班级有学生
  + 学生和课程、圆形和圆环、班级和课程
+ 计算器

```python
from functools import reduce

#格式整理
def exp_fmt(exp):
    while re.search('[+-]{2,}',exp):
        exp.replace('--','+')
        exp.replace('+-','-')
        exp.replace('-+','-')
        exp.replace('++','+')
        return exp

#计算两个数的乘法或除法
def mul_div(exp):
    #'3*4','5/6'
    if '*' in exp:
        a,b=exp.split('*')
        return float(a) * float(b)
    if '/' in exp:
        a, b = exp.split('/')
        return float(a) / float(b)



#计算表达式中所有加减法
def remove_addsub(exp):
    ret=re.findall('[-+]?\d+(?:\.\d+)?',exp)
    # count=0
    # for i in ret:
    #     count+=float(i)
    # print(count)
    res=reduce(lambda a,b:float(a)+float(b),ret)
    return res

#计算表达式中的所有乘除法
import re
def remove_muldiv(exp):
    while True:
        ret=re.search('\d+(\.\d+)?[*/]-?\d+(\.\d+)?',exp)
        if ret:
            son_exp=ret.group()
            print([son_exp])
            res=mul_div(son_exp)
            print(res)
            exp=exp.replace(son_exp,str(res))
            print('-->',exp) #1+12.0*5/6
        else:
            break
    return exp


#计算乘除法
ret=remove_muldiv('1+3*4*5/6')
print(ret)
#计算加减法
exp='1+2.238-++317+-428-5+6'
exp=exp_fmt(exp)
ret=remove_addsub(exp)
print(ret)

# 下一步
# 计算加减乘除四则运算的表达式
# 并去括号
```



# 今日内容

+ 面向对象三大特性：
  + 继承
  + 封装
  + 多态

+ 继承

  ```python
  # 猫：
  #    吃
  #    喝
  #    睡
  #    爬树
  # 狗：
  #    吃
  #    喝
  #    睡
  #    看家
  class Cat:
      def __init__(self,name):
          self.name=name
      def eat(self):
          print('%s eat'%self.name)
      def drink(self):
          print('%s drink'%self.name)
      def sleep(self):
          print('%s sleep'%self.name)
      def climb(self):
          print('%s climb'%self.name)
  
  
  class Dog:
      def __init__(self, name):
          self.name = name
      def eat(self):
          print('%s eat' % self.name)
      def drink(self):
          print('%s drink' % self.name)
      def sleep(self):
          print('%s sleep' % self.name)
      def house_keep(self):
          print('%s house_keep' % self.name)
  
  #上面两个类有重叠部分
  
  小白=Cat('小白')
  小白.eat()
  小白.drink()
  小白.sleep()
  小白.climb()
  
  小黑=Dog('小黑')
  小黑.eat()
  小黑.drink()
  小黑.sleep()
  小黑.house_keep()
  
  #继承----需要解决代码的重复
  #继承语法：
  class A:
      pass
  class B(A):
      pass
  #B继承A，A是父类，B是子类
  #A是父类、基类、超类
  #B是子类、派生类
  
  #对于上述猫狗的代码，可以定义一个父类,把重复的放在父类
  class Animal:
      def __init__(self, name):
          self.name = name
      def eat(self):
          print('%s eat' % self.name)
      def drink(self):
          print('%s drink' % self.name)
      def sleep(self):
          print('%s sleep' % self.name)
  
  class Cat(Animal):
      def climb(self):
          print('%s climb'%self.name)
  
  class Dog(Animal):
      def house_keep(self):
          print('%s house_keep' % self.name)
  ```

  子类可以使用父类中的方法

  子类和父类中有相同方法时，会优先从自己的类空间找方法，即只使用子类的方法。

  + 有时，子类想要调用父类方法的同时，还想要执行自己的同名方法。

    + 在自己的eat方法中调用父类的方法，此时self.eat应改为Animal.eat

    ![image-20200704121541780](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200704121541780.png)

     

  + 父类和子类方法的选择：

    + 自己有，用自己的
    + 自己没有，用父类的
    + 自己有还想用父类的，self换成父类名

+ #多继承：有好几个爹（java不支持多继承，py支持）

**内容补充**

+ object类 类祖宗
  所有在python3中的类，都是继承object类的
  object中有init
  所有的类都默认继承object
+ 类中的绑定方法和普通函数
  + 类调用函数是普通函数：A.eat()
  + 对象调用函数是绑定方法：a.eat()

+ 类中很有必要添加注释，写在类的开头或函数的开头

+ pickle

  ```python
  #pickle
  class Course:
      def __init__(self,name,period,price):
          self.name=name
          self.period=period
          self.price=price
  
  # python=Course('python','6 month',21800)
  import pickle
  # with open('pickle_file',mode='wb')as f:
  #     pickle.dump(python,f)
  with open('pickle_file','rb')as f:
      while True:
          try:
              #可迭代取内容
              python=pickle.load(f)
              print(python.name)
              print(python.price)
  ```

# 明日学习

队列、栈、多继承等

## 代码总行数2538+164=2702行