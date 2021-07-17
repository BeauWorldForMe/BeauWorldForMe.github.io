System.out.println等

![image-20210512171937857](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210512171937857.png)

![image-20210513143120926](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210513143120926.png)

# File类的使用

+ 相关记录或放在一起的数据的集合
+ java.io.File
+ 绝对路径和相对路径
  + 在同一目录下 使用相对路径
  + getPath获取相对路径
  + getAbsolutePath获取绝对路径
  + isAbsolute是不是绝对路径

# 字节流

+ ![image-20210514122819306](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210514122819306.png)

+ FileInputStream

  + 读取图像数据之类的原始字节流
  + 从文件系统中的某个文件中获得输入字节
  + read
  + close

+ FileOutputStream

  + write
  + close

+ 字节流适合文件复制等 不适合存数据，字符流适合存数据，因为字节流容易在存储时因为编码原因数据变化

+ 复制时 可能比原文件数据大

  + 可以使用

    ```
    fos.write(b,0,n);
    ```

  
  ## 缓冲流
  
  write
  
  flush清空，清空后自动执行写操作，写入文件
  
  close也会清空缓冲区
  
  输入-缓冲区-输出-缓冲区

# 字符流

+ Reader输入流

+ Writer输出流

+ 适用于字符的传递

+ ## 字节字符转换流

  练习在imooc8

# 对象序列化

+ 步骤：
  + 创建一个类，继承Serializable接口
  + 创建对象
  + 将对象写入文件
  + 从文件读取对象信息
+ 对象输入流ObjectInputStream
+ 对象输出流ObjectOutputStream
+ 练习在imooc9

