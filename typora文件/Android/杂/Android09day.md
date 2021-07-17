## Android应用程序剖析

在运行应用之前，你需要知道Android项目中的一些文件目录和文件 -



![Hello World示例](https://www.runoob.com/wp-content/uploads/2015/05/hello_word1.jpg)

| 序号 | 文件夹、文件和说明                                           |
| :--- | :----------------------------------------------------------- |
| 1    | src:包含项目中所有的.java源文件，默认情况下，它包括一个 MainActivity.java源文件对应的活动类，当应用程序通过应用图标启动时，将运行它。 |
| 2    | gen:这包含由编译器生成的.R文件，引用了所有项目中的资源。该文件不能被修改。 |
| 3    | bin:这个文件夹包含Android由APT构建的.apk包文件，以及运行Android应用程序所需要的其他所有东西。 |
| 4    | res/drawable-hdpi:这个目录下包括所有的为高密度屏幕设计所需的drawable对象。 |
| 5    | res/layout:这个目录存放用于定义用户界面的文件。              |
| 6    | res/values:这个目录存放各种各样的包含一系列资源的XML文件，比如字符串和颜色的定义。 |
| 7    | AndroidManifest.xml:这个是应用程序的清单文件，描述了应用程序的基础特性，定义它的各种组件。 |