# 内容回顾

re模块的常用方法

+ findall（正则，待匹配字符串，flag）：返回所有匹配项的列表
+ search：返回一个变量，通过group取到第一个匹配项
+ match：从头开始找第一个，其他同search
+ finditer：返回一个迭代器，通过迭代再group取到一个变量
+ compile（正则）同一个正则表达式要多次使用，提前编译节约时间
+ split：通过正则表达式匹配的内容进行分割
+ sub：替换，通过正则表达式匹配的内容进行替换
+ subn：替换，在sub基础上返回一个元组，第一项内容是替换结果，第二项是替换次数

标签匹配+身份证号匹配例子

分组命名 取消分组优先

+ （?P<组名>正则）（?P=组名）(?:正则)

```python
# 匹配年月日日期 格式2018-12-6
[1-9]\d{3}-(1[0-2]|0?[1-9])-[[12]\d|3[01]|0?[1-9]]

# 匹配邮箱地址
[-\w.]+@([-\da-zA-Z]+\.)+[a-zA-Z\d]{2,6}
```

# 今日内容

递归函数I

+ ```python
  #递归问题，os模块：查看一个文件夹下所有文件，这个文件夹下面还有文件夹，不能用walk
  #D:\Typora
  import os
  def show_file(path):
      name_lst=os.listdir(path)
      for name in name_lst:
          abs_path=os.path.join(path,name)
          if os.path.isfile(abs_path):
              print(name)
          elif os.path.isdir(abs_path):
              show_file(abs_path)
  show_file('D:\Typora')
  ```

+ ```python
  #递归问题，计算斐波那契数列，找第100个数
  #1 1 2 3 5
  def fib(n,a=1,b=1):
      if n==1 or n==2:
          return b
      else:
          return fib(n-1,b,a+b)
  ret=fib(100)
  print(ret)
  ```

+ ```python
  #递归问题，os模块：计算一个文件夹下所有文件的大小，这个文件夹下面还有文件夹，不能用walk
  #D:\Typora
  import os
  def dir_size(path):
      size=0
      name_lst=os.listdir(path)
      # print(name_lst)
      for name in name_lst:
          abs_path=os.path.join(path,name)
          if os.path.isfile(abs_path):
              size += os.path.getsize(abs_path)
          else:
              ret=dir_size(abs_path)
              size += ret
      return size
  
  ret=dir_size('D:\Typora')
  print(ret)
  ```

shutil模块

+ 拷贝文件：shutil.copy2(原文件，现文件)
+ 拷贝目录：shutil.copytree(原目录，现目录，ignore=xx)
+ 删除目录：shutil.rmtree(目录，ignore=xx)
+ 移动文件/目录：shutil.move
+ 获得磁盘的使用空间
+ 压缩文件夹：shutil.make_archive(压缩文件名，格式，路径)
+ 解压：shutil.unpack_archive(压缩文件)

logging模块

+ 为什么要写log？

  + log是为了排错
  + log用来做数据分析

+ 举例：购物商城

  + 什么时间买了什么商品
  + 把哪些商品加入了购物车
  + 一个用户登录时间地点
  + 搜索了什么
  + 什么时候关闭了软件
  + **上述等操作都存到了数据库**
  + 做数据分析的内容--**记录到日志**

  如果学生管理系统被某人删了某些东西，日志都有

+ 用来记录用户的行为 - 数据分析

+ 用来记录用户的行为 - 操作审计

+ 排查代码中的错误

+ 

```python
import logging
#输出内容是有等级的：默认处理warnning级以上的信息
logging.debug('debug message')            #调试
logging.info('info message')              #信息
logging.warning('warning message')        #警告
logging.error('error message')            #错误
logging.critical('critical message')      #批判性

#无论希望日志里打印哪些内容，都得自己写，没有自动生成日志的事儿
```

+ 日志等级的设置

  + logging.basicconfig(format='',datefmt='')

  + ```python
    import logging
    logging.basicConfig(format='%(asctime)s-%(name)s-%(levelname)s-%(module)s:%(message)s',
                        datefmt='%Y-%m-%d %H:%M:%S %p',
                        )
    logging.warning('warning message test2')
    ```

    ```python
    #输出到文件,并且设置信息等级，handlers=[放文件操作符]
    import logging
    fh=logging.FileHandler('tmp.log',encoding='utf-8')
    sh=logging.StreamHandler()
    logging.basicConfig(format='%(asctime)s-%(name)s-%(levelname)s-%(module)s:%(message)s',
                        datefmt='%Y-%m-%d %H:%M:%S %p',
                        level=logging.DEBUG,
                        handlers=[fh,sh]
                        )
    logging.warning('warning message test2')
    logging.error('error message test2')
    logging.critical('critical message test2')
    ```

  + 日志的切分

# 明天学习

面向对象

## 代码总行数2325+75=2400行