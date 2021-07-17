# 回顾

+ int str bool
+ str: s1='tangdaren123'
  + 索引：
    + s1[0]
    + s1[-1]
    + s1[:3]
    + s1[:5:2]
    + s1[-1:-4:-1]
    + s1[-1:-6:-2]
  + 常用操作方法：
    + upper、lower
    + startswith、endswith（返回bool）
    + split 默认按照空格分割，可指定分隔符将str分割成list
    + strip默认去除字符串两边空格换行符制表符
    + isdecimal isalpha isalnum
    + format格式化输出
    + count数出字符串中某元素出现次数
    + join 连接，将list------>str
    + replace 替换
    + len() 获取数据的元素个数
+ for循环
  + for i in 可迭代对象

# 练习

```python
#使用for循环对s='321'进行循环，每次打印的内容：倒计时3秒。。。
s='321'
for i in s:
    print('倒计时%s秒'%(i))
print('出发')
#或者
s='321'
for i in s:
    print('倒计时{}秒'.format(i))
print('出发')
```

# 分享

#### 如何学习python

python：语言，中文、英语。

华尔街英语：母式英语

input 听读学      output 写说练

2岁的孩子：听50%、说50%、纠正，半年到一年就学会了一门语言

学习python的比例

+ 每天敲200行代码  现在我235行+以前积累500行=735行

+ 目标10万行

+ 模仿、重复和练习---改动、变通-------创新

  

# Today内容

+ 列表的初识

  + why：int bool str
    + str：存储少量数据，不够开发用
    + str：索引切片等操作返回的都是str，数据类型单一
  + what：list
    + l1=[100,'Henri',True,[1,2,3]]承载任意数据类型，存储大量数据
    + python常用的容器型数据类型。
    + 其他语言：java中叫数组
    + 列表是有序的，可索引、切片（步长）。

+ 列表的索引切片

  + ```python
    l1=[100,'汤达人',True,[1,2,3]]
    #索引
    print(l1[0],type(l1[0]))#100 <class 'int'>
    #切片，顾头不顾腚
    print(l1[:2])#[100, '汤达人']
    
    l2=[1,3,2,'a',4,'b',5,'c']
    print(l2[3:6])#['a', 4, 'b']
    ```

+ 列表的增删改查

  + 增：
    + append()追加
    + insert()按位置加
    + extend()迭代追加

  ```python
  # 增删改查，容器型数据类型都能作增删改查
  l3=['汤达人','天津大学','周老师','实验','数据']
  # 增
  # append：追加
  print(l3.append('xx'))##None 打印这个是没用的，要打印原list
  print(l3)#['汤达人', '天津大学', '周老师', '实验', '数据', 'xx']
  
  #应用：
  l3=['汤达人','天津大学','周老师','实验','数据']
  while 1:
      name=input('请输入新员工姓名：(q退出程序)')
      if name.upper()=='Q':
          break
      l3.append(name)
  print(l3)
  ```

  ```python
  #insert，索引位置插入
  l3=['汤达人','天津大学','周老师','实验','数据']
  l3.insert(2,'李老师')
  print(l3)#['汤达人', '天津大学', '李老师', '周老师', '实验', '数据']
  
  #extend:迭代着追加
  l3=['汤达人','天津大学','周老师','实验','数据']
  l3.extend('abcd')
  print(l3)#['汤达人', '天津大学', '周老师', '实验', '数据', 'a', 'b', 'c', 'd']
  l3.extend(['abcd',1,2,3])#['汤达人', '天津大学', '周老师', '实验', '数据', 'a', 'b', 'c', 'd', 'abcd', 1, 2, 3]
  print(l3)
  ```

  + 删：

    + pop()索引删

    + remove()指定元素删（如果有重名元素，默认删除左数第一个）

    + clear()清空

    + del 按索引删，用法不一样了

    + ```python
      #删
      #pop 按照索引位置删除,默认删除最后一个
      l3=['汤达人','天津大学','周老师','实验','数据']
      l3.pop(1)#按照索引删除，返回的是删除的元素
      #print(l3.pop(1)) #天津大学
      print(l3) #['汤达人', '周老师', '实验', '数据']
      
      #del
      l3=['汤达人','天津大学','周老师','实验','数据']
      del l3[3:5]
      print(l3)#['汤达人', '天津大学', '周老师']
      ```

  + 改：

    + 按索引改
    + 按切片改，不用一一对应，个数随意
    + 按切片加步长改，改几个要一一对应

    ```python
    # 改
    # 按照索引改值
    l3=['汤达人','天津大学','周老师','实验','数据']
    l3[0]='xx'#直接改
    print(l3)#['xx', '天津大学', '周老师', '实验', '数据']
    ```

  + 查：

    + 按索引查
    + 按切片步长查
    + for循环查

+ 列表的嵌套

  ```python
  l1=[1,2,'tangdaren',[1,'Henri',3,]]
  #将其中‘tangdaren’变成大写，放回原处
  l1[2]=l1[2].upper()
  print(l1)#[1, 2, 'TANGDAREN', [1, 'Henri', 3]]
  #给小列表[1,'Henri',3,]追加一个元素‘a’
  l1[3].append('a')
  print(l1)#[1, 2, 'TANGDAREN', [1, 'Henri', 3, 'a']]
  #将列表中的‘Henri’通过字符串拼接的方法在列表中变成‘Henrinb’
  l1[3][1]=l1[3][1]+'nb'
  print(l1)#[1, 2, 'TANGDAREN', [1, 'Henrinb', 3, 'a']]
  ```

  ```python
  #练习2
  lis=[2,30,'k',['qwe',20,['k1',['tt',3,1]],89],'ab','adv']
  #将列表lis中的‘tt’变大写
  lis[3][2][1][0]=lis[3][2][1][0].upper()
  print(lis)#[2, 30, 'k', ['qwe', 20, ['k1', ['TT', 3, 1]], 89], 'ab', 'adv']
  #列表中3变成字符串100
  lis[3][2][1][1]='100'
  print(lis)#[2, 30, 'k', ['qwe', 20, ['k1', ['TT', '100', 1]], 89], 'ab', 'adv']
  #列表中字符串1变成数字101
  lis[3][2][1][2]=101
  print(lis)#[2, 30, 'k', ['qwe', 20, ['k1', ['TT', '100', 101]], 89], 'ab', 'adv']
  ```

+ 元组的初识（了解）

  + 只读列表，存大量数据，可以索引切片加步长
  + list的[]变成()就是元组
  + 元组的元素不能增减改
  + 只能查看
  + 但元组里如果有list，list里的元素能改

+ 元组的简单应用（了解）

  + 重要数据：用户名、密码、个人信息，不想让别人改动的一些数据，可以使用元组

  + 元组的拆包。分别赋值

    ```python
    a,b=(1,2)
    print(a,b)
    ```

    这样实现了把元组里的值分别赋给了a和b

    列表也可以实现拆包，但是一般都用元组进行拆包。

+ range()

  ```python
  r=range(10)  # [0,1,2,3,4,5,6,7,8,9]
  #print(r) #顾头不顾腚
  for i in r:
      print(i)
  
  #range()有索引吗？
  print(r[1])  #yes有索引
  
  for i in range(1,101):
      print(i) #打印1~100
  
  for i in range(2,101,2):
      print(i) #打印100内偶数
  
  for i in range(100,0,-1):
      print(i) #打印100~1
  ```

  + 多与for循环结合使用
  + 构建一个带范围的list

  ```python
  l1=[1,2,3,'tangdaren','henri']
  #利用for循环，利用range，将l1列表的所有索引打印
  for i in range(len(l1)):
      print(l1[i])
  ```

# 今日总结

1. list的操作方法要记忆
   + append insert extend pop remove del clear
2. list嵌套
3. range() 和for循环结合

# 明天学习

字典……

