# 回顾

1. pycharm简单使用

2. while循环
   
   + 结构
   
   + pass
   
   + while实现打印1-2+3-4+……+99
   
   + ![image-20200614190433061](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200614190433061.png)
   
     
   
3. 格式化输出：针对str，让字符串中某些位置变为动态可传入的

   + % s str d digist i int
   + %%第二个%转义

4. 编码初识（二进制和文字对应关系）

   1. ASCLL
   2. GBK
   3. Unicode
   4. Utf-8

# 今天内容大纲

1. ## 基础数据类型总览

   + 10203 13 333 2041 **int **进行+-*/
   + '今天吃了吗'  **str **存储少量数据
   + True False    **bool **判断真假
   + [12，True，'汤达人'，[1,2,3]]     **list 列表** 存储大量数据
   + (12,True,'汤达人'，[1，2，3]) **tuple** **元组** 存储大量数据，内部不能改变
   + {'name'：'汤达人'} **dict 字典**存储大量关联型的数据，查询速度快
   + **set 集合**，求交集并集差集等。

2. ## int

   + pycharm中ctrl+左键点击，可以查看类方法

   + 主要用于计算

   + 不同进制的转换。十进制、二进制

     ```python
     '''二进制转换成十进制
     
     0001 1010 ----------->?26
     '''
     b=1*2**4+1*2**3+0*2**2+1*2**1+0*2**0
     print(b)  #26
     ```

     ![image-20200614194133948](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200614194133948.png)

     ```python
     '''十进制转换成二进制
     42------->?
     '''
     i=5
     print(i.bit_length())#有效二进制长度   #3
     ```

3. ## bool

   + bool<--------->int   0,1

4. ## str

   + 索引，切片

     ```python
     s1='python全栈'
     #从左至右有顺序、下标索引012345
     s2=s1[0]
     print(s2,type(s2)) #p <class 'str'>
     
     s3=s1[-1] #从后往前第一个
     print(s3) #栈
     
     #按照切片取值
     s4=s1[0:6]  ##取六个数，顾头不顾腚
     print(s4) #python
     
     s5=s1[6:]##取到最后
     print(s5) #全栈
     
     s6=s1[0:5:2]#第三个数是步长、0可省略
     print(s6) #pto
     
     s7=s1[-1:-5:-1]#倒序取必须有一个倒序步长，但是不加不报错
     print(s7) #栈全no
     
     s8=s1[::-1]
     print(s8) #栈全nohtyp
     ```

   + 常用操作方法

     + upper()、lower()

     ```python
     #字符串常用操作方法
     #不会对原字符串操作，会产生新字符串
     s='TangDaRen'
     s1=s.upper()#全变大写
     s2=s.lower()#全变小写
     print(s1)
     #应用：验证码不区分大小写
     username=input('用户名')
     password=input('密码')
     code='QweA'
     print(code)
     your_code=input('验证码，不区分大小写')
     if your_code.upper()==code.upper():
         if username=='汤达人' and password=='123':
             print('登录成功')
         else:
             print('用户名密码错误')
     else:
         print('验证码错误')
     ```

     + startswith()、endswith()

     ```python
     #starswith endswith
     #返回bool值
     s='TangDaRen'
     print(s.startswith('Ta')) #True
     print(s.startswith('TangDaRen')) #True
     print(s.startswith('a')) #False
     print(s.startswith('a',1,3)) #True（1~3是不是以a开头）
     ```

     + replace()  #替换

     + ```python
       #replase
       msg='Leo is a good boy,Leo,Leo'
       msg1=msg.replace('Leo','Henri')#默认全部替换
       msg2=msg.replace('Leo','Henri',2)#替换两个
       print(msg1)#Henri is a good boy,Henri,Henri
       print(msg2)#Henri is a good boy,Henri,Leo
       ```

     + strip() #去除开头结尾的空白

     ```python
     #strip：开头结尾空格、制表符\t、换行符\n的去除
     msg='     Leo is a good boy,Leo,Leo'
     msg3=msg.strip()
     print(msg3)#Leo is a good boy,Leo,Leo
     #去除指定字符
     msg4=msg.strip('Leo is')
     print(msg4)# a good boy,Leo,
     ```

     + **split()**  分割：默认按照空格分割，返回一个list
       + 可以实现str-------->list

     ```python
     #split
     msg='Leo is a good boy,Leo,Leo'
     msg5=msg.split()
     print(msg5) #['Leo', 'is', 'a', 'good', 'boy,Leo,Leo']
     #指定分隔符
     msg='Leo is a good boy,Leo,Leo'
     msg6=msg.split(',')
     print(msg6)#['Leo is a good boy', 'Leo', 'Leo']
     ```

     + **join()** 非常好用

       + 可以实现list-------->str

       ```python
       #join
       s1='Leo'
       s2='+'.join(s1)
       print(s2,type(s2)) #L+e+o <class 'str'>
       l1=['Leo is a good boy', 'Leo', 'Leo']
       s3=','.join(l1)
       print(s3)#Leo is a good boy,Leo,Leo
       ```

     + count() 数出字符串出现次数

     + format()：格式化输出

       ```python
       #format:格式化输出
       #第一种用法：
       msg7='我叫{}今年{}'.format('Henri','23')
       print(msg7)#我叫Henri今年23
       #第二种用法：带索引，可重复用
       msg8='我叫{0}今年{1}性别{2}，我依然叫{0}'.format('Henri','23','男')
       print(msg8)#我叫Henri今年23性别男，我依然叫Henri
       #第三种用法：带关键字索引，可调顺序
       msg9='我叫{name}今年{age}性别{sex}，我依然叫{name}'.format(age='23',sex='男',name='Henri')
       print(msg9)#我叫Henri今年23性别男，我依然叫Henri
       ```

     + is系列
     
       ```python
       ### is系列
       name='tangdaren123'
       print(name.isalnum())#字符串由字母和数字组成True
       print(name.isalpha())#字符串只由字母组成False
       print(name.isdecimal())#字符串只由十进制组成False
       #应用：购物车
       s1=input('请输入您的金额：')
       if s1.isdecimal():
           print(int(s1))
       else:
           print('输入有误')
       ```
     
       

5. ## for循环

+ in

  + ```python
    s1='天津大学edu'
    print('天'in s1)#True
    print('天津'in s1)#True
    print('天津edu'in s1)#False
    print('天津edu'not in s1)#True
    ```

+ len():获取字符串元素个数

+ for 变量 in interable（可迭代变量）:

  …………………………

  ```python
  s2='天津大学最牛的学生'
  for i in s2:
      print(i)
  '''
  天     s2[0]
  津     s2[1]
  大     s2[2]
  学     …………
  最
  牛
  的
  学
  生
  '''
  ```

  ```python
  s2='天津大学最牛的学生'
  for i in s2:
      print(i)
      if i=='的':
          break
  '''
  天     s2[0]
  津     s2[1]
  大     s2[2]
  学     …………
  最
  牛
  的
  '''
  ```

  