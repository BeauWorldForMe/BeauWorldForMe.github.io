# 昨日回顾

1. 函数的参数：
   1. 实参角度：位置参数、关键字参数、混合参数
   2. 形参角度：位置参数、默认参数、仅限关键字参数、万能参数
   3. 形参角度参数顺序：位置参数，*args，默认参数，仅限关键字参数，**kwargs
2. *的魔性用法
   + 函数定义时：聚合
   + 函数调用时：打散
3. python中存在的三个空间
   + 内置名称空间：存储内置函数：print、input等
   + 全局名称空间：py文件、存放的时py文件（除去函数、类内部的）变量，函数名与函数内存地址的关系
   + 局部名称空间：存放函数内部的变量与值的对应关键，一个函数开辟一个局部名称空间。
4. 三个空间的加载顺序：内置、全局、局部
5. 三个空间的取值顺序：就近原则、LEGB
   1. 局部作用域只能引用全局变量，不能修改
6. 作用域：
   1. 全局作用域
   2. 局部作用域
7. 函数的嵌套
8. globals（）、locals（）

# 今日内容

+ 面试不能说‘可能’两个字

+ 补坑

  ```python
  #补充的知识点（global，nonlocal）
  #坑
  #默认参数的陷阱
  def func(name,sex='男'):
      print(name)
      print(sex)
  func('henri') #这样不报错
  #
  #陷阱只针对于默认参数时可变的数据类型
  def func1(name,alist=[]):
      alist.append(name)
      return alist
  ret=func1('henri')
  print(ret)  #['henri']
  ret2=func1('tangdaren')
  print(ret2) #['henri', 'tangdaren'],这时列表第一次运行的元素没有清空
  ```

  ![image-20200621131158554](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200621131158554.png)

  如果你的默认参数指向的是可变的数据类型，那么你无论调用多少次这个默认参数，在内存中都是同一个

  ```python
  #局部作用域的陷阱
  #1.局部改变全局变量
  #2.在局部作用域先引用后定义
  count=1
  def func():
      print(count)
      count=3 ##先引用后定义会报错
  func()
  ```

  ![image-20200621133916893](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200621133916893.png)

  

1. global nonlocal

   ```python
   #global 全局的
   #在局部作用域生命一个全局变量。
   def func():
       global name
       name='tangdaren'
       print(name)
   func()
   print(name)
   
   #nonlocal 不能操作全局变量
   #用于局部作用域：内层函数对外层函数进行修改
   def wrapper():
       count=1
       def inner():
           nonlocal count
           count += 1
       print(count) #1
       inner()
       print(count) #2
   wrapper()
   ```

2. 函数名的运用

   + 函数名+（）就能执行函数，函数名指向的时函数的内存地址

   + 函数名就是变量

   + 函数名也能作为容器型数据类型的元素

   + 函数名也能作为函数的参数
   + 函数名可以做函数的返回值

3. 新特性：格式化输出

   ```python
   #py3.6x以后才有的格式化输出新特性------前加f或F
   name='aa'
   age=18
   msg=f'我叫{name}，今年{age}'
   
   #可以加表达式
   dic={'name':'henri','age':22}
   msg=f'我叫{dic["name"]},今年{dic["age"]}'
   print(msg)
   
   #还能结合函数写
   ```

   结构简化、效率高、还可以结合表达式和函数

4. 迭代器

+ 可迭代对象

  + 字面意思:
    + 对象？：python中一切皆对象。一个实实在在存在的内容。
    + 可迭代？：更新迭代。重复的，循环的一个过程，每次都有新的内容
    + 可以进行循环更新的一个实实在在的值
  + 专业角度：内部含有`‘__iter__’`方法的对象，就是可迭代对象
  + 目前学过的可迭代对象？str list tuple dict set range 文件句柄等。

+ 获取对象的方法并且以字符串的形式表现：dir()

+ 判断一个对象是否是可迭代对象:

  ```python
  #获取一个对象的所有方法：dir()
  s1='sdiwqjdijfh'
  l1=['a',2,23,4,5,6,7,8,s1]
  a=l1
  if '__iter__' in dir(a):
      print('是可迭代对象')
  else:
      print('不是可迭代对象')
  ```

+ 小结

  + 内部含有`‘__iter__’`方法的对象，就是可迭代对象
  + 可迭代对象优点：
    + 存储的数据能直接显示，比较直观。
    + 拥有的方法较多，操作方便。
  + 可迭代对象缺点：占用内存，不能直接取值，索引(切片)除外。
    + for i in list时，for循环内部把可迭代对象转换成了迭代器才能取。

+ 迭代器

  + 迭代器的定义

    + 字面意思：可更新迭代的工具

    + 专业角度：内部含有`‘__iter__’`方法并且含有`‘__next__’的对象就是迭代器`

    + 目前学的：文件句柄

      ```python
      #判断文件句柄是不是迭代器
      with open('文件1',encoding='utf-8',mode='w') as f1:
          print(('__iter__'in dir(f1))and('__next__'in dir(f1))) #True
      ```

+ 迭代器的取值

  + next()

+ 可迭代对象如何转化成迭代器

  + ```python
    s1='abasdh'
    obj=iter(s1) #就转换成了迭代器
    #或
    obj=s1.__iter__()
    #对迭代器取值，一个next取一个值
    next(obj)
    next(obj)
    next(obj)
    next(obj)
    next(obj)
    next(obj)#一个next对应一个值
    #多了会报错
    ```

+ while循环模拟for循环机制

  ```python
  #while循环模拟for循环机制
  l1=['a',2,23,4,5,6,7,8,10]
  # for i in l1:
  #     print(i)
  #1.将可迭代对象转化成迭代器
  obj=iter(l1)
  #2.取值
  while 1:
      try:
          print(next(obj))
      except StopIteration:
          break
  ```

+ 小结

  + 优点：非常节省内存、惰性机制--next取值绝不多取
  + 缺点：速度慢，不走回头路（而可迭代对象每次迭代从头开始）

+ 可迭代对象与迭代器的对比

  + 可迭代对象是一个操作方法比较多，比较直观，存储数据相对少（几百万个对象，8G内存是可以承受的）的数据集。当侧重于对数据灵活处理，并且内存足够多，可迭代对象好用。
  + 迭代器是一个非常节省内存，可以记录取值位置，但是不直观，方法单一的数据集。当数据量过大，大到足以撑爆内存，迭代器好用。

# 今日总结

1. 默认参数的坑、作用域的坑
2. global nonlocal
3. 格式化输出
4. 函数名的运用
5. 可迭代对象和迭代器：对比、转换、next()取值……

# 明日内容

生成器、列表推导式

## 代码总行数1672+80=1752行