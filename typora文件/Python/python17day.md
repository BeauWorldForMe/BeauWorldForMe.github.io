# 昨日回顾

自定义模块等

# 今日内容

+ 自定义模块

+ 模块是什么？

  + 抖音：20万行代码全部放在一个py文件?

    为什么不行?

    1. 代码多，读取时间长
    2. 代码不容易维护

    所以应该？

    一个py文件拆分100个文件，100个py文件又有相似相同的功能。就需要将相似相同的函数提取出来，放在一个py文件中。

+ 模块分类：

  + 内置模块：200种左右，python解释器自带
  + 第三方模块：一些大牛写的，非常好用的
    + pip install 需要这个指令安装的模块
    + flask、django等等
  + 自定义模块：自己的项目需要，自己写的py文件

+ json pickle模块：序列化模块

  + 将数据结构转换成特殊序列，而且可以反转换回去
  + 为什么存在序列化？
    + 数据存储，str形式
    + 数据通过网络传输，需要--->bytes,但只有str能转换bytes
  + json：python、java公认的特殊的结构
  + pickle：只python

+ thashlib模块

# 今日总结

1. import 三件事情
   + 在内存种创建一个xxx命名的名称空间
   + 执行代码
   + 通过xxx.的方式引用模块里的代码
2. 模块的搜索路径
   1. 先从内存找
   2. 再从sys.path找
3. 序列化模块json***、pickle
4. hashlib：加密模块
   1. 用于密码加密
   2. 用于文件校验

# 明天学习

软件开发规范

## 代码总行数2085行