# 内容回顾

1. 文件操作初识

   三步走：

   + 打开文件open()
     + 文件路径path，编码方式encoding=，mode（默认读）
   + 操作文件(对文件句柄进行操作)
     + 读、写、追加
     + 各四种模式
     + 读：read()、read(n)、readline()返回字符串、readlines()返回列表、for循环
     + 写：没文件创建新文件写入，有文件清空再写入
     + 追加：没文件创建新文件追加内容，有文件直接追加
     + r+：先读后写
     + 其他功能：
       + tell()找光标位置
       + seek()调整光标位置
       + flush()强制刷新
     + with open（） as f1：
     + 文件的改操作
   + 关闭文件。

2. 练习题

   ```python
   #以a+模式打开文件，先追加一行：'汤达人最帅'，然后再从最开始将原内容全部读取出来
   with open('练习文件',encoding='utf-8',mode='a+')as f1:
       f1.write('汤达人最帅')
       f1.seek(0)
       content=f1.read()
       print(content[:-5])
   ```

   ```python
   #通过代码，将a.txt其构建成：[{'name': 'apple', 'price': '10', 'amount': 3}, {'name': 'tesla', 'price': '100000', 'amount': 1}, {'name': 'mac', 'price': '3000', 'amount': 2}, {'name': 'lenovo', 'price': '30000', 'amount': 3}, {'name': 'chicken', 'price': '10', 'amount': 3}]
   #
   l1=[]
   with open('a',encoding='utf-8')as f1:
       for line in f1:
           dic={}
           # print(line,type(line))
           line=line.strip() #apple 10 3
           line_list=line.split()
           print(line_list)
           dic['name']=line_list[0]
           dic['price']=line_list[1]
           dic['amount']=int(line_list[2])
           l1.append(dic)
   print(l1)
   ```

# 今日内容

1. 函数的初识

   + 函数：以功能（完成一件事）为导向，登录，注册，len，一个函数就是一个功能，随调随用
   + 减少代码重复性
   + 增强代码可读性

   ```python
   def meet():
       print('打开抖音')
       print('上滑一下')
       print('下滑一下')
       print('找风景')
       print('点赞')
       print('走起')
   '''
   结构：def关键字，定义函数
       meet函数名：与变量设置相同，具有可描述性
       函数体：缩进。函数中尽量不要出现print
   '''
   
   #函数什么时候执行？
   #当函数遇到   函数名（） 函数才会执行
   meet()
   ```

2. 函数的结构与调用

   函数的结构

   ```python
   def 函数名()：
   
   ​		函数体
   ```

   + 调用一次执行一次

3. 函数的返回值

   + 完成功能后返回的状态
   + return
     + 在函数中，终止函数
     + return可以给函数的执行者返回值
       + return 单个值    
       + return 多个值    元组 

4. 函数的参数

   + 函数执行时写的参数：实参

     + 实参角度：
       + 1.位置参数：几个位置，几个参数，一一对应
       + 2.关键字参数：在执行时使用（形参名='实参'）等形式，不需要按照顺序

   + 函数定义中写的参数：形参

     + 形参角度
       + 1.位置参数
       + 2.默认值参数：设定完不改就设置为默认值，在写函数时，在形参部分就定义了默认值，默认值参数必须放在所有参数最后。

   + 三元与运算符：简单的if else

     + ```python
       c=a if a>b else b
       ```

# 今日总结

1.函数：

​	函数的作用：以功能为导向，减少代码重复，增强可读性

​	函数的结构：函数的执行

​	函数的返回值

​	函数的参数：实参角度、形参角度

## 代码总行数1591+46=1637行