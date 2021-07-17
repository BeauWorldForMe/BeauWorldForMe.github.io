## 之前代码总行数735+133=868

# 内容回顾

1. 列表：容器型数据类型，可以承载大量的数据，有序的数据

   + 增：
     + append 追加
     + insert 插入，按索引增
     + extend 迭代着追加
   + 删：
     + pop 按照索引删除，有返回值，返回
     + remove 按照元素删除
     + clear 清空
     + del 索引、切片（步长）
   + 改:
     + l1[1]='xxx'
     + l1[1:3]='1232ddawfw'
     + l1[1:4:2]='ab'
   + 查：索引、切片、for循环

2. 元组：只读列表、（）、拆包

3. range() :可以看作是一个自己控制范围的数字list

   + 面试题：

     ```python
     l1=range(5)
     print(l1[1:3])   #答案range(1,3)  
     ```

   + 面试题2：

     ```python
     for i in range(1,5,-1):
     	print(i)   #答案什么也没输出，也不报错
     ```

4. 练习题

   ```python
   #实现一个整数加法计算器（两个数相加）:
   #
   #如：content=input('请输入内容:')用户输入5+9或5 +9或5+ 9，分割进行计算
   content=input('请输入内容:')
   l1=content.split('+')
   print(l1)
   result=int(l1[0].strip())+int(l1[1].strip())
   print(result)
   ```

   ```python
   #实现一个整数加法计算器（多个数相加）:
   content=input('请输入内容:')
   l1=content.split('+')
   print(l1)
   result=0
   for i in range(len(l1)):
       result += int(l1[i].strip())
   print(result)
   ```

   ```python
   #计算用户输入的内容有几个整数
   content=input('请输入内容:')
   result=0
   for i in range(10):
       result += content.count('%s'%(i))
   print(result)
   ```

   ```python
   #判断一句话是不是回文
   content=input('请输入内容:')
   if content[::-1]==content:
       print('是回文')
   else:
       print('不是回文')
   ```

   ```python
   #利于下划线将列表连成字符串
   l1=['汤达人','good','boy']
   s1='_'.join(l1)
   print(s1) #汤达人_good_boy
   ```

# 今天学习内容

1. 字典的初识

   + why：

     + 列表可以存储大量数据，但是数据之间的关联性不强
       + ['汤达人'，22，''男'，'Henri',23,男]
     + 列表的查询速度比较慢

   + what：容器型数据类型：**dict**。

   + how：

     + 数据类型的分类（可变与不可变）：

       + 可变（不可哈希）的数据类型：list、dict、set

       + 不可变（可哈希）的数据类型：str、bool、int、tuple

         比如对字符串s的操作，形成了一个新字符串，原字符串不改变。

         ![image-20200615175345422](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200615175345422.png)

       + 字典：{}括起来，以键值对（键:值）存储的数据类型

       ```python
       dic={'汤达人':
            {'name':'tangdaren','age':'22','sex':'男'}
        }
       ```

       + 键：必须是不可变的数据类型：int、str（bool、tuple几乎不用）

         ```python
         #验证字典的合法性
         dic={[1,2,3]:'henri',1:666}
         print(dic) #TypeError: unhashable type: 'list'键是不可哈希的
         ```

       + 值：可以是任意数类型

         ```python
         #键值对：
             #酒店：
             #键：房间号，如0~99。必须唯一，不唯一不报错，会按照后一个的数据走。
             #值：房间：房间里放什么数据都可以。
             #一定是通过键寻找值。
         ```

       + 字典3.5x版本前是无序的

       + 字典3.6x会按照初次建立字典的顺序排列，学术上不认为是有序的

       + 字典3.7x以后都是有序的。

       + 字典的查询速度非常快，存储关联性的数据。

       + 字典的缺点：以空间换时间。

2. 字典的使用（创建、增删改查）

   1. 字典的创建：

      ```python
      #字典的创建：面试可能会考
      #方式一
      dic=dict((('one',1),('two',2),('three',3)))
      print(dic) # {'one': 1, 'two': 2, 'three': 3}
      #方式二
      dic=dict(one=1,two=2,three=3)
      print(dic) # {'one': 1, 'two': 2, 'three': 3}
      #方式三
      dic=dict({'one': 1, 'two': 2, 'three': 3})
      print(dic) #{'one': 1, 'two': 2, 'three': 3}
      ```

   2. 增删改查

      ```python
      ## 增删改查
      dic={'name':'tangdaren','age':'22'}
      # 增
      dic['sex']='男'  #增
      print(dic) #{'name': 'tangdaren', 'age': '22', 'sex': '男'}
      #如果对已存在的键做相同操作，改之。
      dic['age']='23'  #改
      print(dic) #{'name': 'tangdaren', 'age': '23', 'sex': '男'}
      #setdefault 设置默认值、有则不变，无则增加
      dic.setdefault('hobby')
      print(dic) #{'name': 'tangdaren', 'age': '23', 'sex': '男', 'hobby': None}
      dic.setdefault('hobby','溜达')
      print(dic) #{'name': 'tangdaren', 'age': '23', 'sex': '男', 'hobby': None}
      dic.setdefault('feature','handsome')
      print(dic)#{'name': 'tangdaren', 'age': '23', 'sex': '男', 'hobby': None, 'feature': 'handsome'}
      
      # 删
      # pop按照键删除键值对,有返回值，返回值是对应的值。pop是重点***
      dic.pop('feature')
      print(dic)#{'name': 'tangdaren', 'age': '23', 'sex': '男', 'hobby': None}
      #另外，如果给pop设置第二个参数，无论字典中有没有此键，都不会报错，并且会把第二个值返回。
      #clear 清空字典内容
      #dic.clear()
      
      # 改
      dic['name']='xxx'
      print(dic)
      
      # 查
      #方法一，按照键查询值，不建议
      print(dic['hobby']) #None
      #方法二，get，返回值同pop,如果有这个键，返回这个值，如果没有，返回第二个参数
      l1=dic.get('hobb','没有此键')
      print(l1) #没有此键
      ```

      + 三个特殊的

        + key()

          ```python
          # keys()可以把键转化成列表
          print(dic.keys()) #dict_keys(['name', 'age', 'sex', 'hobby'])
          print(list(dic.keys()))      #['name', 'age', 'sex', 'hobby']
          ```

        + value()

          ```python
          # values()可以把值转化成列表
          ```

        + item()

          ```python
          # items()可以把所有键值对转换成列表
          print(dic.items()) #dict_items([('name', 'xxx'), ('age', '23'), ('sex', '男'), ('hobby', None)])
          for key,value in dic.items():
              print(key,value)
          '''又实现了元组拆包，得到了这样的表
          name xxx
          age 23
          sex 男
          hobby None
          '''
          ```

          ```python
          #面试题：a=18,b=12，用一行互换a、b
          a=18
          b=12
          ################a,b=b,a####################
          print(a,b) #12 18
          ```

3. 字典的嵌套

```python
dic={
    'name':'汪峰',
    'age':48,
    'wife':[{'name':'章子怡','age':38},],
    'children':{'girl_first':'小苹果','girl_second':'小怡','girl_third':'顶顶'}
}

#1.获取汪峰的名字
print(dic.get('name'))  #汪峰
#2.获取这个字典{'name':'章子怡','age':38}
print(dic.get('wife')[0])  #{'name': '章子怡', 'age': 38}
#3.获取汪峰妻子的名字
print(dic.get('wife')[0].get('name')) #章子怡
#4.获取汪峰第二个孩子的名字
print(dic.get('children').get('girl_second')) #小怡
```

# 今日总结

+ 字典：查询速度快，数据关联性强。
  + 键
  + 值
  + 增删改查
  + 嵌套

# 明天内容

id is == 小数据池、集合……

## Now代码总行数868+137=1005