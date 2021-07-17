## 异常

程序上的错误，背离我们程序意图的。编译或运行

编译器会帮我们修改编译时的错误

运行时的错误要自己来

比如：

+ 使用空的对象调用方法
+ 数组访问时下标越界
+ 算数运算时除数为0
+ 类型转换时无法正常转型

## 如何处理异常

![image-20210508172833383](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210508172833383.png)

## 异常处理分类

+ 抛出异常
+ 捕获异常
+ 对check型异常必须捕获或者声明抛出
+ 允许忽略不可查的RuntimeException（含子类）和Error（含子类）
+ 五个关键字来实现
  + 捕获异常try、catch、finally
  + 声明异常throws
  + 抛出异常throw

## try、catch、finally

```java
try{
	//代码段1
	//产生异常的代码段2
}catch(异常类型 ex){
	//对异常进行处理的代码段3
}finally{
	//代码段4  无论有没有异常 都会执行
}
```

+ try不能单独使用，必须和catch或finally组合使用

+ ```java
  package com.imooc.test;
  
  import java.util.Scanner;
  
  public class TryDemoOne {
  
  	public static void main(String[] args) {
  		// 接受用户两个整数，输出两数的商
  		Scanner in = new Scanner(System.in);
  		System.out.println("====运算开始====");
  		System.out.println("请输入第一个整数：");
  		try{
  			
  			int a = in.nextInt();
  			System.out.println("请输入第二个整数：");
  			int b = in.nextInt();
  			System.out.println("两数商为："+(a/b));
  			
  		}catch(Exception e) {
  			e.printStackTrace(); //可以打印出错误的堆栈信息
  			System.out.println("程序出错啦");
  		}finally {
  			//finally来保证内部一定执行
  			System.out.println("====运算结束====");
  		}
  		
  	}
  
  }
  ```

  + 也可以根据不同的异常弄不同的输出

  + 可以多个catch一起存在

+ 终止finally执行的方法：System.exit(1)

## throw和throws

+ 通过throws声明将要抛出什么类型的异常
+ 通过throw将产生的异常主动抛出

```java
public void method() throws Exception1,Exception2,Exception3...{
	//代码段1
    throw new 异常类型();
}
```

+ 当方法抛出异常列表中的异常，方法不对这些做处理，而是抛向调用该方法的方法，由它去处理
+ 调用这个方法时 使用try,catch处理，必须处理
+ 可以通过抛出异常完成程序逻辑
+ 比如如果不满足条件，抛出异常，然后在catch中处理
  + throw new Exception("xxxxxxxxxx")
  + 可以通过try..throw...catch
  + 也可以throws...throw 然后在方法调用的地方处理这种异常，谁用谁处理
  + Throwable是Exception的父类，可以抛出父类，所以写Throwable也行

## 自定义异常

制定一个类继承Throwable或Exception

来实现逻辑

## 异常链

捕获一个异常 抛出一个新的（在catch里）

新抛出异常，会导致前面的异常信息丢失，可以在括号里的第二个参数加上变量 就可以保留了





