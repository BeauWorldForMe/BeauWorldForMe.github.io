Spring Boot 对测试的支持不可谓不强大，Spring Boot 内置了7种强大的测试框架：

- JUnit： 一个 Java 语言的单元测试框架
- Spring Test & Spring Boot Test：为 Spring Boot 应用提供集成测试和工具支持
- AssertJ：支持流式断言的 Java 测试框架
- Hamcrest：一个匹配器库
- Mockito：一个 java mock 框架
- JSONassert：一个针对 JSON 的断言库
- JsonPath：JSON XPath 库



 以前spring开发需要配置一大堆的xml,后台spring加入了annotaion，使得xml配置简化了很多，当然还是有些配置需要使用xml,比如申明component scan等。

​    Spring开了一个新的model spring boot,主要思想是降低spring的入门，使得新手可以以最快的速度让程序在spring框架下跑起来。

​    那么如何写Hello world呢？

Hello之步骤:
(1)新建一个Maven Java 工程
(2)在pom.xml文件中添加Spring Boot Maven依赖
(3)编写启动类
(4)运行程序

 

​       

 

**1.2 Hello之New**

​    这个步骤很简单，相比大家都会，小编在此为了文档的完整性，稍作简单说明：

首先使用IDE（Eclipse,MyEclipse）工具新建一个Maven工程，可以是Maven Java Project,也可以是Maven Web Project,随便取一个工程名称。我使用的是MyEclipse，工程名是spring-boot-hello1。

 

**1.3 Hello之Maven**

​    第二步，在pom.xml中引入spring-boot-start-parent,spring官方的解释叫什么stater poms,它可以提供dependency management,也就是说依赖管理，引入以后在申明其它dependency的时候就不需要version了，后面可以看到。

Xml代码 [![收藏代码](https://www.iteye.com/images/icon_star.png)](javascript:void())

1. **<****parent****>** 
2.    **<****groupId****>**org.springframework.boot**</****groupId****>** 
3.    **<****artifactId****>**spring-boot-starter-parent**</****artifactId****>** 
4.    **<****version****>**1.3.3.RELEASE**</****version****>** 
5. **</****parent****>** 

 

 

**1.4 Hello之maven web**

​    第三步，因为我们开发的是web工程，所以需要在pom.xml中引入spring-boot-starter-web,spring官方解释说spring-boot-start-web包含了spring webmvc和tomcat等web开发的特性。

 

Xml代码 [![收藏代码](https://www.iteye.com/images/icon_star.png)](javascript:void())

1. **<****dependencies****>** 
2.    **<****dependency****>** 
3. ​     **<****groupId****>**org.springframework.boot**</****groupId****>** 
4. ​      **<****artifactId****>**spring-boot-starter-web**</****artifactId****>** 
5. ​    **</****dependency****>** 
6. **</****dependencies****>** 

 

**1.5 Hello之Maven Run Application**

​    如果我们要直接Main启动spring，那么以下plugin必须要添加，否则是无法启动的。如果使用maven 的spring-boot:run的话是不需要此配置的。（我在测试的时候，如果不配置下面的plugin也是直接在Main中运行的。）

Xml代码 [![收藏代码](https://www.iteye.com/images/icon_star.png)](javascript:void())

1. **<****build****>** 
2.    **<****plugins****>** 
3. ​      **<****plugin****>** 
4. ​        **<****groupId****>**org.springframework.boot**</****groupId****>** 
5. ​        **<****artifactId****>**spring-boot-maven-plugin **</****artifactId****>** 
6. ​     **</****plugin****>** 
7. ​    **</****plugins****>** 
8. **</****build****>** 

 

**1.6 Hello之coding**

​    第四步，真正的程序开始啦，我们需要一个启动类，然后在启动类申明让spring boot自动给我们配置spring需要的配置，比如：@SpringBootApplication,为了可以尽快让程序跑起来，我们简单写一个通过浏览器访问hello world字样的例子：

Java代码 [![收藏代码](https://www.iteye.com/images/icon_star.png)](javascript:void())

1. @RestController 
2. @SpringBootApplication 
3. **public** **class** App { 
4.   
5.  @RequestMapping("/") 
6.  **public** String hello(){ 
7.   **return** "Hello world!"; 
8.  } 
9.   
10.  **public** **static** **void** main(String[] args) { 
11. ​     SpringApplication.run(App.**class**, args); 
12.  } 
13. } 

 

其中@SpringBootApplication申明让spring boot自动给程序进行必要的配置，等价于以默认属性使用@Configuration，@EnableAutoConfiguration和@ComponentScan

@RestController返回json字符串的数据，直接可以编写RESTFul的接口；

 

**1.7 Hello之Run**

​    第五步，就是运行我们的Application了，我们先介绍第一种运行方式。第一种方式特别简单：右键Run As -> Java Application。之后打开浏览器输入地址：http://127.0.0.1:8080/ 就可以看到Hello world!了。第二种方式右键project – Run as – Maven build – 在Goals里输入spring-boot:run ,然后Apply,最后点击Run。

 

1.8 Hello之Error

​    顺利的情况下当然是皆大欢喜了，但是程序吧往往会给你开个小玩笑。那么我们要注意什么呢？主要是jdk的版本之类的，请看官方说明：

 


![img](http://dl2.iteye.com/upload/attachment/0116/6586/d745e178-b945-33d1-91f8-119d1f05c9e8.png)