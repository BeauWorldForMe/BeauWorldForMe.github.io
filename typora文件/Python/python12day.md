# 昨日回顾

1. 可迭代对象：

   + 可以更新迭代的实实在在的值。
   + 内部含有`'__iter__'`方法。
   + str、tuple、dict、set、range
   + 优点：操作方法多，灵活直观
   + 缺点：占用内存。

2. 迭代器：

   + 可以更新迭代的一个工具（数据结构）
   + 内部含有`'__iter__'`并且含有`'__next__'`方法。
   + 文件句柄
   + 优点：节省内存，惰性机制
   + 缺点：不直观，速度相对慢，操作方法单一，不走回头路。

3. 格式化输出

4. 函数名的运用：就是个变量

5. 作用域的坑

6. 练习题

   ```python
   #看代码写结果
   def func1():
       print('in func1')
   
   def func2(x):
       print('in func2')
       return x
   
   def func3(y):
       print('in func3')
       return y
   
   ret=func2(func1)
   ret()
   ret2=func3(func2)
   ret3=ret2(func1)
   ret3()
   '''
   in func2
   in func1
   in func3
   in func2
   in func1
   '''
   ```

   ```python
   #看代码写结果
   def func():
       for item in range(10):
           pass
       print(item)
   func()
   '''
   9
   '''
   ```

   ```python
   #看代码写结果
   l1=[]
   def func4(args):
       l1.append(args)
       return l1
   print(func4(1))
   print(func4(2))
   print(func4(3))
   '''
   [1]
   [1,2]
   [1,2,3]
   '''
   ```

   ![image-20200622102000781](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200622102000781.png)

   ```python
   #写函数计算阶乘
   def cal(num):
       count=1
       for i in range(num,0,-1):
           count = count * i
       return count
   print(cal(3))
   ```

# 今日内容

1. 生成器

   ```python
   #吃包子,5000个，函数剩下没吃完不好算
   def func1():
       l1=[]
       for i in range():
           l1.append(f'{i}号包子')
       return l1
   ret=func()
   print()#就是个可迭代对象
   
   #吃包子，吃一个做一个，生成器
   def gen_func1():
       for i in range(1,5001):
           yield f'{i}号包子'
   ret=gen_func1()
   for i in range(200):
       print(next(ret)) ##next一次做一个包子
       #就是个迭代器
   ```

   + 什么是生成器：生成器和迭代器可以看作一种，生成器的本质就是迭代器。

   + 生成器迭代器区别：生成器是我们自己用python代码构建的数据结构。而迭代器都是提供或转换来的。

   + 获取方式

     + 生成器函数

       ```python
       #以往见到的函数
       def func():
           print(111)
           print(222)
           return 3
       ret=func()
       print(ret)
       '''
       111
       222
       3
       '''
       
       #生成器函数
       def func():
           print(111)
           print(222)
           yield 3
           yield 4
           yield 5
       ret=func()
       print(ret) #<generator object func at 0x000002B0868AB0F8>
       print(next(ret)) #一个next对应一个yield
       # 111
       # 222
       # 3
       print(next(ret)) # 4
       print(next(ret)) # 5
       ```

     + 生成器表达式

     + python内部提供的一些

   + yield

   + yield、return对比

     + yield：函数中有yield就一定式生成器函数而不是函数了。生成器函数可存在多个yield，yield不结束生成器函数。
     + return：函数中只存在一个return，结束函数返回值。

   + yield from

     ```python
     #yield from
     def func2():
         l1=[1,2,3,4,5]
         yield from l1  
         ##这样会从列表中拿出单一的元素，将l1这个列表变成了一个迭代器
     ret=func2()
     print(next(ret))
     ```

2. 生成器表达式、列表推导式

   + 列表推导式：用一行代码构建一个比较复杂有规律的列表。

     ```python
     l1=[i for i in range(1,11)]
     ```

     + 列表推导式分两类：

       + 循环模式：

         `[变量（加工后的变量）for 变量 in iterable]`

       + 筛选模式：

         ```python
         #30以内能被3整除的数
         l1=[i for i in range(1,31) if i%3==0]
         ```

         ```python
         #过滤长度小于3的字符串列表,并将剩下的转换成大写
         l1=['sadjiwqf','sd','a','dqwdj','asd','wqewr','henri']
         print([i.upper() for i in l1 if len(i)>=3])
         ```

   + 生成器表达式：与列表推导式的写法几乎一样，把[]变成（）就变成了生成器表达式，非常节省内存，也有筛选模式和循环模式。

     ```python
     obj=(i for i in range(1,11))
     next(obj)
     ```

   + 小结：

     + 列表推导式：

       + 缺点：有毒，列表推导式只能构建比较有规律的列表。超过三层循环才能构建成功的不建议用，另外debug模式查找错误不行。

       + 优点：简单、装逼。

         ```python
         #装逼
         #构建一个列表[2,3,4,5,6,7,8,9,10,'J','Q','K','A']
         l1=[i for i in range(2,11)]+list('JQKA')
         print(l1)
         ```

     + 列表推导式与生成器表达式区别

       + 写法上:[],()
       + iterable、iterator

     + (了解)还有字典推导式、集合推导式，都是一行构建

3. 内置函数I

   #python提供了68个内置函数
   #今天的这部分大部分了解即可。

   + eval()剥去字符串的外衣，运算里面的代码。最好不要使用

     ```python
     #eval
     s1='1+3'
     print(eval(s1)) #4
     ```

   + exec()：与eval()几乎一样，但是是处理代码流的。

   + hash()：获取一个对象的哈希值。int str bool等

   + help()：获取对象的使用方法

   + callable():判断对象是否可调用

# 今日总结

1. 生成器：我们用python代码自己构建的
2. 生成器函数yield
3. yield与return区别、yield from
4. 列表推导式、生成器表达式
5. 内置函数：学了一些了解即可的

# 明天学习

1. lambda表达式
2. 内置函数II
3. 闭包

## 代码总行数1752+135=1887行