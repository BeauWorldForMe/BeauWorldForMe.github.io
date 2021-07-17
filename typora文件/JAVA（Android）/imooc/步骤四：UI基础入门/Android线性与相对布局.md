# Activity

+ Activity类是一个可视化的界面类
+ 其实就是定义了一个普通的类，继承Activity类，普通类就有了可视化界面的特征
+ 其中onCreate方法是继承自父类的方法，一进入程序马上调用，相当于java的main方法
  + 初始化和设置写入这里
  + setContentView设置内容视图的id
    + R.layout.activity_main 这是一个id，是在R文件生成的layout类别中的一个属性
    + R文件是自动生成的，不能去修改，是final修饰的，不能被继承
    + R：为每一个资源文件按类别分配一个索引，通过索引反向寻找资源文件

# 布局

通过一个个的标签来设置布局

+ 线性布局LinearLayout
+ 相对布局
+ 帧布局
+ 表格布局TableLayout
+ 网格布局GridLayout
+ 约束布局

添加方式

+ xml文件设计
+ java代码（不直观）
+ 

![image-20210521163555870](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210521163555870.png)

+ match_parent
+ wrap_content
+ 数值，单位用dp（xml用）
+ 字体大小用sp

![image-20210521165505682](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210521165505682.png)

```
android:layout_margin="20dp" //外边距
android:padding="20dp" //内边距
android:layout_weight //权重,设置了权重的控件会后摆放，按比例摆放要把对应的宽或高调为0dp
android：layout_gravity //重力，调整布局向哪边靠
```

**权重要和0dp搭配**

重力，调整布局向哪边靠，当前控件相对父容器的摆放重力

![image-20210521173104923](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210521173104923.png)

alignTop和上边线对其

toLeftOf在xxx左边

![image-20210521174428590](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210521174428590.png)

