## Math类 

+ Java系统提供的类

+ abs绝对值

+ pow(2,3)幂次

+ round四舍五入

+ random一个0，1之间的随机数

+ ···

+ 使用方法

  ```
  Math.abs(-12)
  ```

## 函数

之前用到的·操作，是让对象做的操作，点后的内容，是在类中存在的函数，也可以说是方法

```java
//判断素数
package sushu_hanshu;

import java.util.Scanner;

public class Main {
	public static boolean isPrime(int i) {
		//判断i是不是素数的函数
		boolean isPrime = true;
		for(int k=2;k<i;k++) {
			if (i%k ==0) {
				isPrime = false;
				break;
			}
		}
		return isPrime;
	}
	
	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);
		int m = in.nextInt();
		int n = in.nextInt();
		if(m==1) m=2;
		int cnt=0;
		int sum=0;
		for(int i=m;i<=n;i++) {
			if(isPrime(i)) {
				//调用函数判断
				cnt++;
				sum+=i;//求素数和
			}
		}
		System.out.println("在"+m+"和"+n+"中间有"+cnt+"个素数，总和为"+sum);
	}
}
```

+ 函数是一块代码，接受零个或多个参数，做一件事情，并返回0个或者1个值
+ 前面要有public static是函数头
+ `return；`或者`return a；`
+ 函数有多个出口是不好的习惯
+ java语言永远只能传值给函数
+ 函数每次调用都会有自己的新空间
+ 变量的生存期：什么时候这个变量出现，什么时候这个变量消亡
+ 变量的作用域：在什么范围内可以访问这个变量
+ **对于本地变量----在大括号内生存作用**
+ 不能在一个块里定义同名变量
+ 参数在进入函数的时候被初始化了

