![image-20210713183737058](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713183737058.png)

需要在类中有一个无参构造器

![image-20210713191918455](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713191918455.png)

通过全类名来配置，会自动构造一个无参的对象，对象名为id名，通过property设置其中的属性

![image-20210713192249537](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713192249537.png)



![image-20210713192656478](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713192656478.png)

![image-20210713192103562](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713192103562.png)

![image-20210713192122332](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713192122332.png)

![image-20210713192153121](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713192153121.png)

![image-20210713192831918](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713192831918.png)

property属性注入

使用构造器注入👇

![image-20210713193429605](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713193429605.png)

![image-20210713205737765](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713205737765.png)

![image-20210713205824599](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713205824599.png)

![image-20210713210046928](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713210046928.png)

![image-20210713210342223](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713210342223.png)

![image-20210713212249659](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713212249659.png)

![image-20210713212951675](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713212951675.png)

![image-20210713213211140](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713213211140.png)可以用util把集合独立出来，然后这个集合就可以被多个bean共享

![image-20210713213536837](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713213536837.png)

![image-20210713213812937](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713213812937.png)

![image-20210713220744937](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713220744937.png)

![image-20210713221647539](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210713221647539.png)

自动装配如果要用 就都要用，而且byName和byType不能一起用