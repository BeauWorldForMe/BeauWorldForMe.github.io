# View

+ 处理文本内容的View（TextView）
+ 被点击的View（Button）
+ 处理图片内容的View（ImageView）
+ 接收用户信息输入的View（EditText）
+ 进度条类的View（ProgressBar）

![image-20210522104417557](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210522104417557.png)

![image-20210522104732649](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210522104732649.png)

所有控件都继承于View

![image-20210522110032381](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210522110032381.png)

ScrollView里只能有一个直接子控件

```java
singleLine = “true” //单行后面省略
ellipsize=“start” //设置省略号位置，start middle end
focusable = "true" //文字跑马灯获取焦点
focusableIntouchMode = //设置触摸时可以获取焦点位置
marqueeRepeatLimit  //设置跑马灯重复次数
//只能有一个跑马灯效果,因为需要有焦点 一个屏幕只有一个焦点
```

# EditText

+ android:inputType输入类型
+ android:hint启示文字
+ android:maxLength输入长度

# Button

+ 注册点击事件
  + 自定义内部类
  + 匿名内部类
  + 当前Activity实现接口
  + 在布局文件添加点击事件属性

# ImageView

android:src 指定前景图片资源 不会拉伸

android:background 背景 会拉伸

...

#  ImageButton

android:src 指定前景图片资源 不会拉伸

# ProgressBar进度条

默认是圆形，不断旋转的动画效果，style可以调整

```java
style = "?android:attr/progressBarStyleHorizontal" 设置风格
android:progress = “30”
android:max = "200"
android:indeterminate = "true"是否永恒滚动
```

无焦点提示：Toast.makeText(this,"姓名或密码不得为空"，Toast.LENGTH_SHORT);//第三个参数是提示时间