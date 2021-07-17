![image-20210509154244436](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210509154244436.png)

包装类都用final修饰 都没有子类 不能被继承

静态方法既可以通过类名调用，也可以通过对象名调用

## 装箱拆箱

基本数据类型和包装类的转换

+ 自动装箱：

```java
int t1 = 2;
Integer t2 = t1;
```

+ 手动装箱：

```java
int t1 = 2;
Integer t3 = new Integer(t1);
```

+ 自动拆箱

```java
int t4 = t2;
```

+ 手动拆箱

```
int t5 = t2.intValue()  //也可以转为别的类型
```

## 一些方法

Integer.toString(t)

Integer.parseInt(t) //字符串转成Integer，然后再拆箱 可以实现字符串转int

包装类是类，定义的初始值是null

对象常量池（除了Double和Float都可以用）：数值在-128~127之间，可以自动装箱，不在的话 判断值不一定相等的。