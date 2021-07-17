# 内容回顾

1. 数据类型的补充

   + str:pass
   + tuple:
     + (1)----->int
     + count 计数
     + index 通过元组获取索引
   + list
     + sort 排序从小到大
     + sort(reverse=True)排序从大到小
     + 列表相加 列表与数字相乘
     + 循环列表的问题
   + dict
     + update 更新，增加值，修改值，创建字典，将一个字典所有键值对覆盖添加到原字典
     + dict.fromkeys(iterable,value)
       + 如果value是个可变的数据类型，任何一个变，都变
   + 数据类型的转换：
     + 0、{}、[]、set()、''、()、None

2. 编码的进阶

   ​	ASCLL、GBK、Unicode、Utf-8……

   1. 所有编码本（除去Unicode以外），不能直接互相识别
   2. 在内存中所有数据必须是Unicode编码存在，除了bytes类型

   ![image-20200618130518400](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200618130518400.png)

   	3. str----->bytes：encode称为编码，编成计算机看的码，反之decode叫解码，解成人能读的代码

3. 练习题

```python
#看代码写结果
v1=[1,2,3,4,5,6,7,8,9]
v2={}
for item in v1:
    if item<6:
        continue
    if 'k1' in v2:
        v2['k1'].append(item)
    else:
        v2['k1']=[item]
print(v2)   ## {'k1':[6,7,8,9]}
```

```python
#深浅copy相关
import copy
#
v1=[1,2,3,4,5]
v2=copy.copy(v1)
v3=copy.deepcopy(v1)

print(v1[0] is v2[0]) #True
print(v1[0] is v3[0]) #True
print(v2[0] is v3[0]) #True

#
v1=[1,2,3,4,[11,22]]
v2=copy.copy(v1)
v3=copy.deepcopy(v1)

print(v1[-1] is v2[-1]) #True
print(v1[-1] is v3[-1]) #False
print(v2[-1] is v3[-1]) #False
```

```python
#利用python代码构建一个这样的列表(升级题):
#[['_','_','_'],['_','_','_'],['_','_','_']]
print([['_']*3]*3) 
```

```python
#用户输入一个数字,判断这个数是否是水仙花数
#水仙花数是一个三位数,三位数每一位的三次方之和等于这个数.
#
#例如:153=1**3+5**3+3**3
num=input('请输入三位数:') #153\370
count=0
if num.isdecimal():
    for i in num:
        count += int(i)**3
    if count == int(num):
        print('是水仙花数')
    else:
        print('不是水仙花数')
else:
    print('请输入纯数字...')
```

```python
#删除姓李的人
#应该倒序删除,不影响索引值
lst=['李老二','李老师','李星星','麻花疼']
for i in range(len(lst)-1,-1,-1):
    if lst[i].strip()[0]=='李':
        lst.pop(i)
print(lst)  #['麻花疼']
```

```python
#车牌区域划分,现给出以下车牌,根据车牌的信息,分析出各省的车牌持有量.
#
#locals={'沪':'上海','黑':'黑龙江','鲁':'山东','鄂':'湖北','湘':'湖南','京':'北京'}
#cars=['鲁A32444','鲁B12333','京B8989M','黑C49678','黑C46555','沪B22333']
#
#结果:{'山东': 2, '北京': 1, '黑龙江': 2, '上海': 1}
##################################################
locals={'沪':'上海','黑':'黑龙江','鲁':'山东','鄂':'湖北','湘':'湖南','京':'北京'}
cars=['鲁A32444','鲁B12333','京B8989M','黑C49678','黑C46555','沪B22333']
dic={}#在循环中给字典增加键值对
for i in cars:
    if locals[i[0]] not in dic.keys():
        dic[locals[i[0]]]=1  #没有键就创建一个键的思想
    else:
        dic[locals[i[0]]] += 1
print(dic) #{'山东': 2, '北京': 1, '黑龙江': 2, '上海': 1}
##################################################
#另法dic.get()的使用
dic={}
for i in cars:
    dic[locals[i[0]]]=dic.get(locals[i[0]],0)+1
print(dic) #{'山东': 2, '北京': 1, '黑龙江': 2, '上海': 1}
```

# 今日内容

1. 文件操作的初识

   + 歪比巴卜的联系方式.txt

   + 利用python代码写一个很low的软件，去操作文件。

     + 文件路径：path
     + 打开方式：读r、写w、追加、读写、写读……
     + 编码方式：utf-8、gbk、gb2321……

     ```python
     f1 = open('d:\联系方式.txt',encoding='utf-8',mode='r')
     content=f1.read()
     print(content)
     f1.close()
     '''
     open：是一个python内置函数，open底层调用的是操作系统的接口。
     f1：变量，f开头的变量，文件句柄（f1，fh，file_handler,f_h)
     对文件进行的任何操作，都要经过文件句柄,如f1.read()。
     encoding：可以不写，如果不写参数，默认的编码本是操作系统默认的编码。
              windows：默认编码gbk
              linux：默认utf-8
              mac：默认utf-8
     f1.close()：关闭文件句柄
     ```

   + 文件操作的三步骤

     + 1.打开文件。
     + 2.对文件句柄进行相应操作。
     + 3.关闭文件。

   + 报错原因：

     + UnicodeDecodeError：文件存储时与文件打开时编码本运用不一致。
     + 路径找不到问题(解决：路径前加r''，使路径的反斜杠不被理解成特殊用意)

2. 文件操作的读

   r，rb，r+，r+b四种模式

   + r：

   ```python
   ##几个文件在一个文件夹下，路径可写相对路径
   f=open('文件的读',encoding='utf-8')
   content=f.read()
   print(content,type(content))
   f.close()
   '''
   汤达人
   a good boy
   Henri is，too <class 'str'>
   '''
   ```

   ```python
   #read(n) 按照字符读取
   f=open('文件的读',encoding='utf-8')
   content=f.read(5)
   print(content)
   f.close()
   '''
   汤达人
   a
   '''
   ```

   ```python
   #readline()按行读
   f=open('文件的读',encoding='utf-8')
   print(f.readline()) #汤达人
   f.close() 
   ```

   ```python
   #readlines()多行读,放到一个列表里
   f=open('文件的读',encoding='utf-8')
   print(f.readlines())
   f.close() #['汤达人\n', 'a good boy\n', 'Henri is，too']
   ```

   ```python
   ##for读取
   f=open('文件的读',encoding='utf-8')
   for line in f:
       print(line)
   f.close()
   '''
   汤达人
   
   a good boy
   
   Henri is，too
   '''
   ```

   + rb：（read bytes）操作的是非文本的文件。图片、视频、音频。

3. 文件操作的写

   w、wb、w+、w+b四种模式

   ```python
   #创建文件写入内容
   f=open('文件的写',encoding='utf-8',mode='w')
   f.write('随便写一点')
   f.close()
   ```

   ```python
   #有文件,写入内容
   #先清空原文件内容,后写入
   f=open('文件的写',encoding='utf-8',mode='w')
   f.write('今天的学习')
   f.close()
   ```

   ```python
   #以wb写入新文件（非文本）
   f=open('aaa.jpg',mode='rb')
   content=f.read()
   f.close()
   f1=open('bbb.jpg',mode='wb')
   f1.write(content)
   f1.close()
   ```

4. 文件操作的追加

   a、ab、a+、a+b四种模式

   ```python
   #每次运行一遍,会在原文件后面追加写入内容
   f=open('文件的追加',encoding='utf-8',mode='a')
   f.write('不错,确实')
   f.close()
   ```

5. 文件操作的其他模式

   + r+（+就是增加一个功能，r+就是读写操作）

   ```python
   #实现读完并追加,不会清空文件写
   f=open('文件的读写',encoding='utf-8',mode='r+')
   content=f.read() # 光标在哪从哪读
   print(content)
   f.write('得得得得得得得得') # 光标在哪从哪写
   f.close()
   ```

6. 文件操作的其他功能

   总结：

   ​	三个大方向

   读，四种模式：r、rb、r+、r+b

   写，四种模式：w、wb、w+、w+b

   追加，四种模式：a、ab、a+、a+b

   相应的功能：对文件句柄的操作：read、read(n)……

   + **补充：**

   ```python
   # tell()按字节获取光标的位置
   f=open('文件的读写',encoding='utf-8')
   print(f.tell()) #0
   content=f.read()
   print(f.tell()) #59
   f.close()
   
   #seek 调整光标的位置
   f=open('文件的读写',encoding='utf-8')
   print(f.seek(0))  #调整光标的位置是0字节处
   content=f.read()
   print(content)
   f.close()
   
   #flush 强制刷新
   f=open('文件的其他功能',encoding='utf-8',mode='w')
   f.write('sadvvccxefwdsda')
   f.flush()
   f.close()
   ```

7. 打开文件的另一种方式

   ```python
   #with open()
   #优点1:不用手动关闭文件句柄,会在一定时间内关闭
   with open('文件的读',encoding='utf-8')as f1:
       print(f1.read())
   
   #优点2:可操作多个文件句柄
   with open('文件的读',encoding='utf-8')as f1,\
           open('文件的写',encoding='utf-8',mode='w')as f2:
       print(f1.read())
       f2.write('123ewadsafzxcsadadw')
       
   #缺点：待续
   ```

8. 文件的改的操作

   #对文件内容进行修改步骤：
   1.以读的模式打开原文件.
   2.以写的模式创建一个新文件.
   3.将原文件的内容读出来,修改成新内容,写入新文件.
   4.将原文件在内存中删除.
   5.将新文件重命名成原文件.

   ```python
   #将'歌词'文件中所有的'哈哈'改成'Henri'
   #low版，因为read大文件不好用，而for好用
   import os
   # 1.以读的模式打开原文件.
   # 2.以写的模式创建一个新文件.
   with open('歌词',encoding='utf-8')as f1,\
       open('歌词.bak',encoding='utf-8',mode='w')as f2:
   # 3.将原文件的内容读出来,修改成新内容,写入新文件.
       old_content=f1.read()
       new_content=old_content.replace('哈哈','Henri')
       f2.write(new_content)
   # 4.将原文件在内存中删除.
   # 5.将新文件重命名成原文件.
   os.remove('歌词')
   os.rename('歌词.bak','歌词')
   ```

   ```python
   #进阶版，使用for
   import os
   # 1.以读的模式打开原文件.
   # 2.以写的模式创建一个新文件.
   with open('歌词',encoding='utf-8')as f1,\
       open('歌词.bak',encoding='utf-8',mode='w')as f2:
   # 3.将原文件的内容读出来,修改成新内容,写入新文件.
       for line in f1:
           #old_line=line.strip()
           new_line=old_line.replace('Henri','哈哈')
           f2.write(new_line)
   # 4.将原文件在内存中删除.
   # 5.将新文件重命名成原文件.
   os.remove('歌词')
   os.rename('歌词.bak','歌词')
   ```

   + 有关清空的问题

     关闭文件句柄再次以w模式打开才涉及清空，不关闭则看光标位置读写。

# 今日总结

+ 文件操作：
  + **r** w a rb wb r+ ab重点记
  + read() wirte tell seek flush
  + 文件的改的代码（重点）。

# 明天学习

+ 函数的初识

## Now代码总行数1349+242=1591行