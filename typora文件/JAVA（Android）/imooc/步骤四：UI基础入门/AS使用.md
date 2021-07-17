+ Android树下，按类别进行了分类
  + Gradle单独放配置文件
  + manifests目录放配置文件
  + java目录放源文件
    + 第一个目录下放源码
  + res目录放资源文件
    + drawable放图像图形资源，其中是xml文件编写
    + layout放布局资源
    + mipmap直接放图像图形资源
    + values放常量资源（颜色，字符串，风格）
+ Project树中展示真实物理结构（硬盘中存储位置）

# 编程时需要关注的几处

+ Activity
+ layout
+ AndroidManifest.xml



# 程序运行时

第一步，读取AndroidManifest.xml声明文件，其中要有注册的Activity

```java
<intent-filter>
    <action android:name="android.intent.action.MAIN" />

    <category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
```

上面为启动界面的注册内容

然后会进入第二步，读Activity中程序

```java
setContentView(R.layout.activity_main);
```

然后回进入第三步，进入activity_main中

# Gradle

Android主流的编译工具

项目有：setting.gradle用于记录哪些module要加入编译过程、build.gradle中的配置会应用于所有module

Module有:build.gradle各自的配置

+ minSdkVersion:最小API level
+ compileSdkVersion：编译的SDK版本，建议用最新的
+ targetSdkVersion：目标版本，指定运行程序时的API版本 
+ dependencies：依赖配置，依赖的库

# AVD

genymotion、夜神等也可以

# 常用技巧

快捷键设置

+ setting-keymap-class name Completion 
+ 格式化代码ctrl+alt+l
+ 撤销ctrl+z 反撤销ctrl+shift+z
+ 弹提示alt+/
+ 代码自动修正alt+enter
+ 文档性说明ctrl+q
+ 查找ctrl+f
+ 按关键字全局搜索ctrl+shift+f

调试技巧

+ log写日志
+ debug断点调试

![image-20210518195527009](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210518195527009.png)



# gradle更新问题

+ 没办法打开代理通道
  + 修改gradle路径 setting-Gradle-改成本地
    + D:\Android\Android Studio\ruanjian\gradle\m2repository\com\android\tools\build\gradle\3.4.1
  + 修改项目下gradle-wrapper.properties最后一行，换成当前工具版本的路径
  + 项目的build.gradle文件的依赖，改成本地有的版本号
+ gradle一直处于更新状态
  + 当项目低于工具版本：修改项目下gradle-wrapper.properties最后一行改成这里面的版本D:\Android\Android Studio\ruanjian\gradle
  + 手动下载项目下gradle-wrapper.properties最后一行的版本gradle，放在D:\Android\Android Studio\ruanjian\gradle
  + 项目下gradle-wrapper.properties最后一行的https改为http
+ gradle project sync failed....导入module时易出现
  + show log in explore-idea.log看底部信息
  + 打开导入module的build.gradle文件，修改其中compileSdkVersion、buildToolsVersion版本为D:\Android\AndroidSDK\platforms中有的，然后把下面的dependencies修改为和原项目相同

# 中文乱码问题

UTF-8支持中文

+ setting-File encodings

  + IDE Encoding工具编码
  + Project Encoding项目编码
  + File or Director Encoding和Property File Encoding文件目录编码

+ 单个java右键File Encoding

+ 手动配置：在对应的Module的gradle中添加

  ```java
  compileOption.encoding = "GBK"
  ```

  