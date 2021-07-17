# 内容回顾

面向对象

+ 类：是具有相同属性和相似功能的一类事物
+ 对象/实例：具体的，一类可以有多个对象
+ 实例化

练习

```python
# 定义一个圆形类，半径是这个圆的属性，实例化一个半径为5的圆形，一个半径为10的圆形
# 完成方法：
    # 计算圆形面积
    # 计算圆形周长
from math import pi
class Circle:
    def __init__(self,r):
        self.r=r
    def area(self):
        return pi * self.r ** 2
    def perimeter(self):
        return pi * self.r * 2

c=Circle(5)
print(c.r)
print(c.area())
print(c.perimeter())

c.r=10
print(c.r)
print(c.area())
print(c.perimeter())
'''
5
78.53981633974483
31.41592653589793
10
314.1592653589793
62.83185307179586
'''
```

```python
# 定义一个用户类，用户名和密码是这个类的属性，实例化两个用户，分别有不同的用户名和密码
    #登录成功之后才创建用户对象
    #设计一个方法修改密码
import os

def login(name,passwd,filepath='userinfo'):
    with open(filepath,encoding='utf-8')as f:
        for line in f:
            user,pwd=line.strip().split('|')
            if user==name and pwd==passwd:
                return True
            else:
                return False
class User:
    def __init__(self,username,password):
        self.user=username
        self.pwd=password
    def change_pwd(self):
        oldpwd=input('请输入原密码')
        newpwd=input('请输入新密码')
        with open('userinfo',encoding='utf-8')as f1,open('userinfo.bak',mode='w',encoding='utf-8')as f2:
            for line in f1:
                username,password=line.strip().split('|')
                if username==self.user and password==oldpwd:
                    line='%s|%s\n'%(username,newpwd)
                f2.write(line)
        os.remove('userinfo')
        os.rename('userinfo.bak','userinfo')

name=input('请输入用户名')
passwd=input('请输入密码')
ret=login(name,passwd)
if ret:
    print('登录成功')
    obj=User(name,passwd)
    res=obj.change_pwd()
    if res:print('修改成功')
```

# 今日内容

计算器I

```python
#计算两个数的乘法或除法
def mul_div(exp):
    #'3*4','5/6'
    if '*' in exp:
        a,b=exp.split('*')
        return float(a) * float(b)
    if '/' in exp:
        a, b = exp.split('/')
        return float(a) / float(b)

#计算表达式中的所有乘除法
import re
# exp='1+3*4*5/6'
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
ret=remove_muldiv('1+3*4*5/6')
print(ret)
```

python里的大问题

+ 知道类，知道这个类有什么属性xxxx，有了对象才知道具体的值。
+ 数据类型相关
+ python中一切皆对象，对象的类型就是类
+ 在class中：
  + 变量的定义叫静态变量/静态属性，存储在类的命名空间
  + 函数的定义叫绑定方法，存储在类的命名空间

+ 面向对象的命名空间：
  + 对象中的变量只属于对象本身，每个对象有属于自己的空间来存储对象的变量
  + 当使用对象名去调用某一个属性，会优先在自己的空间中寻找，找不到再去对应的类中寻找，再找不到才报错
  + 对于类来说，类中的变量，所有对象都可以读取
  + 所有和静态变量相关的增删改查都应用类名处理，而不是对象名直接修改。
+ 组合：
  + 一个类的对象，是另一个类对象的属性

# 今日总结

计算器I

组合

面向对象的命名空间

# 明日学习

继承等

## 代码总行数2442+96=2538行