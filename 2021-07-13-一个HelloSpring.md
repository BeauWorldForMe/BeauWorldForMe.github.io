```java
package com.spring.beans;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		
		
//		//1创建HelloWorld的对象
//		HelloWorld helloWorld = new HelloWorld();
//		//2为name赋值
//		helloWorld.setName("mzwl");
		
		//1.创建Spring的IOC容器对象
		//2.从IOC容器获取Bean实例
		ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
		HelloWorld helloWorld = (HelloWorld) ctx.getBean("helloWorld");
		
		//调用方法
		helloWorld.hello();
	}

}
```

```java
package com.spring.beans;

public class HelloWorld {
	private String name;
	public void setName(String name) {
		this.name = name;
	}
	public void hello() {
		System.out.println("hello"+name);
	}
		
}

```

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	
	<!-- 配置bean -->
	<bean id="helloWorld" class="com.spring.beans.HelloWorld">
		<property name="name" value="Spring"></property>
	</bean>

</beans>

```

![image-20210713172058709](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713172058709.png)



![image-20210713172111954](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713172111954.png)

