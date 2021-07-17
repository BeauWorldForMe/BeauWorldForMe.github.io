# String

是一个字符串处理**类**

+ 创建
  + String s1 = "xxx";
  + String s2 = new String();
  + String s3 = new String("xxx")
+ 常用方法
  + length()
  + charAt()按位置索引字符
  + indexOf()查内容第一次出现的位置
  + lastindexOf()查内容最后一次出现的位置
  + substring()取子串
  + trim()去除两端空格
  + getBytes()转换成二进制字节byte数组）
    + 可以再通过String str1 = new String(arrs,"GBK")转回字符串，称解码，要保持字符集的一致，不然有乱码
  + toUpperCase()
  + toLowerCase()
  + replace()

+ String创建之后是不可变的，修改后都是创建了新对象

## StringBuilder

StringBuilder没有不可变性

StringBuffer是前身，线程安全，而StringBuilder性能更高

+ 常用方法
  + toString()
  + append()
  + delete(a,b)
  + insert(i,str)
  + replace

