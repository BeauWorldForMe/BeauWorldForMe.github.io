# 回顾

1. id == is：

   + ==： 数值是否相同
   + is： 内存地址是否相同
   + id： 获取对象的内存地址

2. 代码块：

   + 一个文件、交互式命令一行都是一个代码块

3. 同一代码块下缓存机制（字符串驻留机制）

   + 所有数字，bool，几乎所有的字符串
   + 优点：提升性能，节省空间

4. 不同代码块的缓存机制（小数据池）

   + 在内存中开辟两个空间，一个空间存储-5~256的int，一个空间存储一定规则的字符串。
   + 如果代码中遇到了满足条件的数据，直接引用提前创建的。
   + -5~256的int，bool，满足一定规则的字符串。
   + 优点：相同

5. 集合set：列表去重，关系测试（交并差）

6. 深浅copy：

   + 浅copy：在内存中开辟一个新的空间存放copy的对象（列表，字典），但里面所有元素与被copy对象里面的元素共用一个。
     + 两内部元素地址是一样的
     + 当被copy对象中追加元素，copy得到的不增加元素
     + 当被copy对象中嵌套的list追加元素，copy里也增加元素
   + 深copy
     + 在外层里的地址就不一样了
       + 不可变的数据类型沿用之前
       + 可变的数据类型自己开辟

7. 练习题

   ```python
   import copy
   l1=[1,2,3,[11,22]]
   # l2=l1.copy()
   l2=copy.copy(l1)
   print(id(l1[-1]),id(l2[-1])) #两个地址是一样的
   ```

   ```python
   #看代码写结果
   data_list=[]
   for i in range(10):
       data={}
       data['user']=i
       data_list.append(data)
   print(data_list)
   '''
   [{'user':0},{'user':1},{'user':2},{'user':3},{'user':4},{'user':5,{'user':6},{'user':7},{'user':8},{'user':9}]
   '''
   ```

   ```python
   #用代码验证‘name'在字典的键中
   info={'name':'aa','hobby':'bb','age':18}
   print('name' in info.keys()) #True
   ```

   ```python
   #循环提示用户输入，输入内容追加到列表，输入n或N结束
   flag=False
   l1=[]
   while flag==False:
       content=input('请输入内容（n或N结束）：')
       if content.upper()=='N':
           flag=True
       else:
           l1.append(content)
           print(l1)
   ```

   ```python
   #循环提示用户输入，输入内容添加到集合，输入n或N结束
   flag=False
   l1=[]
   while flag==False:
       content=input('请输入内容（n或N结束）：')
       if content.upper()=='N':
           flag=True
       else:
           l1.append(content)
           s1=set(l1)
           print(s1)
   ```

   ```python
   #看代码写结果
   #
   v1='人生苦短，我用python'
   v2=[1,2,3,4,v1]
   v1='人生苦短，用毛线python'
   
   print(v2)  #[1,2,3,4,'人生苦短，我用python']
   ```

   ```python
   #看代码写结果
   #
   info=[1,2,3]
   userinfo={'account':info,'num':info,'money':info}
   info.append(9)
   print(userinfo) #{'account':[1,2,3,9],'num':[1,2,3,9],'money':[1,2,3,9]}
   ```

   ```python
   #看代码写结果
   #
   info=[1,2,3]
   userinfo={'account':info,'num':info,'money':info}
   info='题怎么这么多'
   print(userinfo) #{'account':[1,2,3],'num':[1,2,3],'money':[1,2,3]}
   ```

   ```python
   #看代码写结果
   data_list=[]
   data={} #在循环外，每次地址指向的都是同一个字典
   for i in range(10):
       data['user']=i
       data_list.append(data)
   print(data_list)
   '''
   [{'user':9},{'user':9},{'user':9},{'user':9},{'user':9},{'user':9},{'user':9},{'user':9},{'user':9},{'user':9}]
   '''
   ```

   

# 今日内容

1. 基础数据类型的补充

   + str

   ```python
   #str：补充方法，练习一遍
   #
   #capitalize(),首字母大写，其余小写
   s1='tangDAren'
   print(s1.capitalize()) #Tangdaren
   
   #swapcase 大小写翻转
   #
   print(s1.swapcase()) #TANGdaREN
   
   #title 每个单词首字母大写,以非字母元素隔开就行，比如数字
   #
   msg='henri is a good boy'
   print(msg.title()) #Henri Is A Good Boy
   
   #center 居中
   #
   print(s1.center(20,'*')) #*****tangDAren******
   
   #find index 从字符找索引,找左起第一个，如果找不到返回-1
   #
   print(s1.find('a')) # 1
   print(s1.find('o')) # -1
   #index同find，但是找不到会报错
   ```

   + tuple

   ```python
   #tuple
   #
   #元组中如果只有一个元素，没逗号不是元组
   tu1=(2)
   print(tu1,type(tu1)) #2 <class 'int'>
   #
   #count 计数
   #index 索引，找到第一个就返回
   ```

   + list

   ```python
   #list
   #
   l1=[1,23,4,56,78,44,3,2]
   #index 索引，找到第一个就返回
   #
   #sort 排序
   l1.sort() #默认从小到大
   l1.sort(reverse=True) #从大到小
   #
   #reverse 翻转，倒过来
   l2=[1,2,3]
   #列表相加
   print(l1+l2)
   #可以与数字相乘
   print(l1*3)  #把列表复制三次，不是内部乘
   #倒序删除元素
   l3=[11,22,33,44,55]
   for i in range(len(l3)-1,-1,-1):
       if i%2==1:
           l3.pop(i)
   print(l3)  #[11, 33, 55]
   ```

   + dict

   ```python
   #dict补充
   #
   dic={'name':'Henri','age':18}
   #update 增或改的实现，还能把一个元组里的字典加到原字典里，能用另一个字典改原字典的值
   #更新，有则覆盖，无则添加
   #fromkeys 来自键
   dic=dict.fromkeys('abc',100)
   print(dic) #{'a': 100, 'b': 100, 'c': 100}
   # 坑：
   dic=dict.fromkeys([1,2,3],[]) #公用一个空列表，指向的地址一样
   dic[1].append(666)
   print(dic) #{1: [666], 2: [666], 3: [666]}
   ```

   ```python
   #练习：将字典中键含有’k‘元素的键值对删除
   # (注意：循环字典时不能改变字典大小)
   #（但是可以循环列表时改变字典大小）
   #这个挺有意思的
   dic={'k1':'aa','k2':'bb','k3':'cc','asd':'dd'}
   #法1
   l1=[]
   for key in dic:
       if 'k' in key:
           l1.append(key)
   for i in l1:
       dic.pop(i)
   print(dic) #{'asd': 'dd'}
   #
   #法2
   dic={'k1':'aa','k2':'bb','k3':'cc','asd':'dd'}
   for key in list(dic.keys()):
       if 'k' in key:
           dic.pop(key)
   print(dic) #{'asd': 'dd'}
   ```

   

2. 数据类型之间的转换

   + 所有数据都能转换成bool
     + 0，'',(),[],{},set{},None

3. 数据类型的分类（了解）

   + 按可变不可变分类
     + 可变：列表，字典
     + 不可变：int，str，bool，tuple
   + 按访问顺序分类
     + 直接访问：数字
     + 顺序访问：str、list、tuple
     + key值访问：dict

4. 编码的进阶

   + **ASCLL：包含英文字母，数字，特殊字符与010101的关系**
     + a 01000001 一个字符一个字节表示
   + **GBK：只包含本国文字（以及英文字母、数字、特殊字符）与010101的关系**
     + a 一个字符一个字节
     + 中 一个字符两个字节
   + **Unicode：包含全世界所有文字与010101的关系**
     + a 四个字节
     + b 四个字节
     + 中 四个字节
   + **UTF-8：包含全世界所有文字与010101的关系**
     + a 一个字符一个字节
     + To（欧洲文字：葡萄牙西班牙等）一个字符两个字节
     + 中 一个字符三个字节

   1. 不同的密码本之间能否互相识别?不能。

   2. 数据在内存中全部以Unicode编码的，但是当数据用于网络传输或存储到硬盘中，必须是以非Unicode编码。

      + 当编辑内容时，是Unicode编码
      + Ctrl+s保存时，就存成了别的编码

      ![image-20200617121233012](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200617121233012.png)

      + 在内存中有一个数据类型例外，不是Unicode编码，**bytes**

      + ```python
        # 英文时：
        #content：'hello'
            #在内存中的编码方式：Unicode
            #表现形式：'hello'
            #内存中的Unicode编码要转换成非Unicode
        #想要发送，要先转换成bytes数据类型
        #bytes
        b=b'hello'
        print(b,type(b))
        ```

      + ```python
        # 中文时：
        #content：'中国'
            #在内存中的编码方式：Unicode
            #表现形式：'中国'
            #内存中的Unicode编码要转换成非Unicode
        #想要发送，要先转换成bytes数据类型
        #bytes
            # 内存中编码方式：非Unicode #Utf-8
            # 表现形式：b'\xe4\xb8\xad\xe5\x9b\xbd'
        ###############################################
        s1='中国'
        b1=s1.encode('utf-8')  #编码
        print(b1,type(b1)) #b'\xe4\xb8\xad\xe5\x9b\xbd' <class 'bytes'>
        #bytes------>str
        b1=b'\xe4\xb8\xad\xe5\x9b\xbd'
        s2=b1.decode('utf-8')  #解码
        print(s2,type(s2)) #中国 <class 'str'>
        ###############################################
        ##实现gbk----->utf-8
        ##先解码到Unicode
        ##再编码成utf-8
        b1=b'\xd6\xd0\xb9\xfa'
        s=b1.decode('gbk')
        print(s) #中国
        b2=s.encode('utf-8')
        print(b2) #b'\xe4\xb8\xad\xe5\x9b\xbd'
        ```

# 总结

+ 数据类型的补充：
  + list（sort、reverse、列表的相加、乘、循环问题）
  + dict（update、循环问题）
+ 编码的进阶：
  + 要知道bytes类型为什么存在？
  + 以及str-------->bytes（Unicode------->非Unicode）
  + gbk<------->utf-8

# 明天内容

+ 文件的操作

## Now代码总行数 1180+169=1349行