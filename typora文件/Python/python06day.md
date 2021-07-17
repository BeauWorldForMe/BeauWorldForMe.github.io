## Now代码1005行

# 回顾

1. 字典的初识

   + 查询速度快，{'name':'tangdaren'}，存储大量关联型数据
   + 键：int、str（bool tuple不常用）不可变的数据类型
   + 值：任意数据类型
   + 3.5x前无序，3.6x按照初始时的顺序排列，3.7x有序

2. 字典的增删改查

   + 增：setdefault（）设置默认值，有则不变、无则增加
   + 删：pop（）按照键删（可设置返回值）clear del
   + 改：dic['name']='henri'
   + 查：get
   + 特殊：keys() value() items()

3. 字典的嵌套。

4. ```python
   #面试题，字符串处理成字典
   msg='k:1|k1:2|k2:3|k3:4'
   #分割
   msg=msg.strip()
   msg=msg.split('|')
   print(msg) #['k:1', 'k1:2', 'k2:3', 'k3:4']
   #对每个元素操作，for循环
   dic={}
   for i in msg:
       #每次循环以冒号分离
       key,value=i.split(':')
       dic[key.strip()]=int(value)
   print(dic) #{'k': 1, 'k1': 2, 'k2': 3, 'k3': 4}
   ```

# 今日内容

1. is == id用法

   + id：相当于身份证号，唯一，获取内存地址id()

     ![image-20200616143103848](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200616143103848.png)

     ```python
     #id身份证号,内存地址
     s='asdawq'
     print(id(s)) #2667094447640
     
     #==
     l1=[1,2,3]
     l2=[1,2,3]
     print(l1==l2) ##==比较的是两边值是否相等
     
     s1='henri'
     s2='henri '
     print(s1==s2) #False
     
     #is
     l1=[1,2,3]
     l2=[1,2,3]
     print(id(l1))  #1315641372232
     print(id(l2))  #1315641372424
     print(l1 is l2)  #False #is判断的是内存地址是否相同
     ```

     + id相同，值一定同，反之，不一定

2. 代码块

   + 所有代码都需要依赖代码块执行

   + 块是一个python程序的文本，是作为一个单元执行的
   + 一个模块、一个函数、一个类、一个文件都是一个代码块
   + 交互式命令下一行就是一个代码块。

3. 两个机制：同一个代码块下，有一个机制。不同的代码块下，遵循另一个机制。

   ![image-20200616145755716](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200616145755716.png)

4. 同一代码块下的缓存机制

   + 前提条件：同一代码块内
   + 机制内容：pass
   + 适用的对象：int bool str
   + 具体细则：所有的数字，bool，几乎所有的str
   + 优点：提升性能、节省内存

5. 不同代码块下的缓存机制（小数据池）

   ![image-20200616150958493](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200616150958493.png)

   + 前提条件：不同代码块里
   + 机制内容：pass
   + 适用的对象：int bool str
   + 具体细则：**-5~256的数字**、满足一定规则的字符串
   + 优点：提升性能、节省内存

6. 总结

   + 面试题考
   + 回答的时候要分清楚：同一个代码块下适用一个缓存机制，不同代码块下适用另一个机制
   + 小数据池：数字范围-5~256

7. python基础数据类型之：集合set(了解)。容器型数据类型

   + 它要求里面的元素是不可变的数据类型。int str bool tuple
   + 但是它本身是可变的。
   + 集合是无序的
   + {}其中放元素是集合，放键值对是字典

   1. 集合的作用
      + 列表的去重
      + 关系测试：交集、并集、差集……
   2. 集合的创建

   ```python
   ##集合的创建
   #set1=set({1,3,'henri',False})
   #法2
   set1={1,3,'henri',4,5,1,'F',False}
   print(set1)  #无序的
   ```

   ```python
   #空集合的表示
   set()
   print(set(),type(set())) #set() <class 'set'>
   ```

   	3. 集合有效性测试

   ```python
   # 集合的增删
   set1={'henri','tangdaren','F',1,2,3,4,5,23}
   # 增 
   # add
   set1.add('xx')
   # update迭代着增
   
   # 删 
   # remove按元素删
   
   # 不能改，只能先删再增，变相改值
   ```

   4. 交并差

      ```python
      ##交并差
      set1={1,2,3,4,5,6,7}
      set2={3,4,5,6,7,8}
      #交集
      print(set1 & set2) #{3, 4, 5, 6, 7}
      #并集
      print(set1 | set2) #{1, 2, 3, 4, 5, 6, 7, 8}
      #差集
      print(set1 - set2) #{1, 2}
      #反交集,找出不共有的元素
      print(set1^set2) #{1, 2, 8}
      
      #子集<
      print(set1<set2) #False
      #超集>
      print(set1>set2)
      ```

   5. 列表去重，把list先转换成集合，再转回list

8. 深浅copy（面试会考）

   + 赋值运算

     ![image-20200616163714905](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200616163714905.png)

     ```python
     #赋值运算
     l1=[1,2,3,[22,33]]
     l2=l1
     l1.append(666)
     print(l1) #[1, 2, 3, [22, 33], 666]
     print(l2) #[1, 2, 3, [22, 33], 666]
     ```

   + 浅copy

     ```python
     #浅copy
     l1=[1,2,3,[22,33]]
     l2=l1.copy()
     l1.append(666)
     print(l1) #[1, 2, 3, [22, 33], 666]
     print(l2) #[1, 2, 3, [22, 33]]
     
     #另一种情况，说明浅copy外壳不同，但里面元素是共用的
     l1=[1,2,3,[22,33]]
     l2=l1.copy()
     l1[-1].append(666) #大列表中嵌套的小列表里追加元素
     print(l1) #[1, 2, 3, [22, 33, 666]]
     print(l2) #[1, 2, 3, [22, 33, 666]]
     ```

     ![image-20200616164226874](D:\Typora\文件\image-20200616164226874.png)

     ![image-20200616164631984](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200616164631984.png)

   + 深copy

     ```python
     #深copy
     import copy
     l1=[1,2,3,[22,33]]
     l2=copy.deepcopy(l1)
     l1[-1].append(666)
     print(l1) #[1, 2, 3, [22, 33, 666]]
     print(l2) #[1, 2, 3, [22, 33]]
     ```

     ![image-20200616165211687](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200616165211687.png)

     python对深copy做了优化，不可变的数据类型共用，可变的自己用自己的

     ```python
     #这是浅copy
     l1=[1,2,3,[22,33]]
     l2=l1[:]
     l1[-1].append(666)
     print(l1) #[1, 2, 3, [22, 33, 666]]
     print(l2) #[1, 2, 3, [22, 33, 666]]
     ```

     + 浅copy：list、dict：嵌套的可变的数据类型是同一个
     + 深copy：list、dict：嵌套的可变的数据类型不是同一个

# 总结

+ id is ==三个方法
+ 回答的时候要分清楚：同一个代码块下适用一个缓存机制，不同代码块下适用另一个机制
+ 小数据池：数字范围-5~256
+ 优点：提升性能、节省内存
+ 集合：列表去重，关系测试。
+ 深浅copy：理解浅copy

# 练习

```python
#看代码写结果
v={}
for index in range(10):
    v['users']=index
print(v)
'''
{'user':9}
'''
```

```python
#
goods=[
    {'name':'电脑','price':1999},
    {'name':'鼠标','price':10},
    {'name':'游艇','price':20},
    {'name':'手机','price':998},
]
#1.按‘序号 名称 价格’显示
#想显示每个商品，for
for i in range(len(goods)):
    print(i+1,goods[i]['name'],goods[i]['price'])
#2.用户输入选择的商品序号，然后打印商品名称以及商品价格
#用户输入，input
#3.如果用户输入序号有误，提示输入有误，并重新输入
#4.用户输入Q或者q，退出程序。
#upper或lower
flag=False
while flag==False:
    count=input('请输入你选择的商品序号(按q或Q退出)：')
    if count.upper()=='Q':
        break
    elif count=='1' or count=='2' or count=='3' or count=='4':
        print(goods[int(count) - 1]['name'], goods[int(count) - 1]['price'])
        flag = True
    else:
        print('输入序号有误，请重新输入。')
```

# 明天内容

1.基础数据内容补充

2.编码进阶

## 代码总数1005+175=1180行