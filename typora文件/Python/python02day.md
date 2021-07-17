# 回顾

1.编译型和解释型

+ 编译型：一次性编译成二进制，再执行
  + 执行效率高，但不能跨平台，开发效率低
  + 代表语言：C
+ 解释型：逐行解释成二进制，再执行
  + 可以跨平台，开发效率高，但执行效率低
  + 代表语言：python

2.变量

+ 数字、字母、下划线的组合
+ 不能数字开头
+ 不能用python关键字：print、if……
+ 不能用中文
+ 描述性

3.常量

+ 与变量几乎一样

4.基础数据类型

+ int、str、bool……

5.用户输入input

```python
name=input('请输入姓名')
print(type(name))
```

6.if、elif、else……



# 今日学习大纲

1. pycharm的安装和简单使用
   + 辅助开发软件（代码逐行调试、debug模式（）显示中间结果等）
   + 公认最好用
   + ctrl+/注释这行
   + ctrl+d等同Notepad++
2. 格式化输出
3. while循环
4. 运算符and or not
5. 编码的初识

# 内容

## 1.while循环

+ ```python
  # 基本结构
  '''
  while 条件：
      循环
  '''
  ```

![image-20200614130220588](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200614130220588.png)

![image-20200614132825015](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200614132825015.png)



+ 循环终止

  + 改变条件

    ```python
    flag = True
    while flag:
        print('月亮之上')
        print('庐州月')
        print('我们不一样')
        flag = False
        print('人间')
        print('狼的诱惑')
    ```

  + break

    + 循环中遇到break直接退出整个循环体

      ![image-20200614134629034](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200614134629034.png)

  + continue

    + 在循环遇到continue中直接进行下一循环，此次循环结束

    + 相当于到了while循环的底部

    + ```python
      # 05使用continue
      flag=True
      while flag:
          print(111)
          print(222)
          flag=False
          continue
          print(333)
      ```

  + 系统命令

+ while else

  + while循环如果被break打断，就不执行else了

  ```python
  count=1
  while count<5:
  	print(count)
  	if count==2:
  		break
  	count=count+1
  else:
  	print（‘ok’）
  ```

+ where：需要重复之前的动作，输入用户名密码等，考虑while循环。

## 2.格式化输出

```python
#制作一个公共模板,让一个字符串中的某些字符变成动态的

name = input('请输入你的姓名：')
age = input('请输入你的年龄：')
job = input('请输入你的工作：')
Hobby = input('请输入你的爱好：')
# %占位符 s-->str
msg='''-----------info of %s--------------
Name : %s
Age  : %s
Job  : %s
Hobby: %s
-----------------end----------------------'''%(name,name,age,job,Hobby)
print(msg)
```

+ 双百分号转义

  ```python
  msg = '我叫%s，今年%s，学习进度1%%'%('哏啾啾',22)
  ```

+ 将字符串中部分变成动态可传入的，考虑格式化输出

## 3.编码的初识

计算机存储文件、存储数据，以及将一些数据信息通过网络发送出去，存储发送数据的内容，底层都是01010101.

密码本：承载0101和文字的关系

+ ### 最早期的密码本ASCII码：只包含：英文字母、数字、特殊字符。

​	0000 0001：          a

​	0000 0101：          ；

原为7位，最左边预留了1位，所以最左边全是0

8bit==1byte （8位==1个字节）

‘hello123’：8byte、64bit

+ ### 中国的密码本：gbk，也叫国标：包括英文字母、数字、特殊字符和中文

  + 一个英文字母：1byte
  + 一个中文：2byte 00000000 01010101，
    + 2^16个=65535个中文字

+ ### 国际通用密码本：Unicode（万国码）：把世界上所有文字都记录到这个密码本

  + 起初一个字符用2个字节表示：
    + 如a：0000 0001 0000 0011
    + 如中：0000 0001 0100 0001
  + 但是不够，为了涵盖全部文字，用4个字节表示
    + 如a：0000 0001 0000 0011 0000 0001 0000 0011
    + ……
  + 浪费空间、浪费资源
  + 进行升级出现了Utf-8密码本

+ ### Utf-8：最少用8bit，即1个字节表示一个字符

  + 0000 0011：   							a  1个字节
  + 0000 0011 0000 0011：       欧洲 2个字节
  + 0000 0011 0000 0011 0000 0011：中文 3个字节

#### ‘中国12he’：

+ GBK：8个字节
+ UTF-8：10个字节

#### 换算：

8bit=1byte

1024byte=1kB

1024KB=1MB

1024MB=1GB

1024GB=1TB

1024TB=1PB

……

# 明日内容

1. 二进制和十进制转换
2. str bool int转换
3. str具体操作方法：索引切片步长……
4. for循环