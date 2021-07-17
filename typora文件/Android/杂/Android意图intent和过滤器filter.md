# Android 意图(Intent)和过滤器(Filter)

Android意图是一个要执行的操作的抽象描述。它可以通过 startActivity 来启动一个活动，broadcastIntent 来发送广播到任何对它感兴趣的广播接受器组件，startService(Intent) 或者bindService(Intent， ServiceConnection, int) 来与后台服务通讯。

**意图本身（一个 Intent 对象）是一个被动的数据结构，保存着要执行操作的抽象描述。**

例如，你有一个活动，需要打开邮件客户端并通过 Android 设备来发送邮件。为了这个目的，你的活动需要发送一个带有合适选择器的 ACTION_SEND 到 Android 意图处理者。指定的选择器给定合适的界面来让用户决定如何发送他的邮件数据。

```java
Intent email = new Intent(Intent.ACTION_SEND, Uri.parse("mailto:"));
email.putExtra(Intent.EXTRA_EMAIL, recipients);
email.putExtra(Intent.EXTRA_SUBJECT, subject.getText().toString());
email.putExtra(Intent.EXTRA_TEXT, body.getText().toString());
startActivity(Intent.createChooser(email, "Choose an email client from..."));
```

上面的语法调用 startActivity 方法来开启邮件活动，代码运行结果看起来像这样：

![image](https://www.runoob.com/wp-content/uploads/2015/06/send_email.jpg)

例如，你有一个活动，需要在 Android 设备上通过浏览器打开一个URL。为了这个目的，你的活动发送 ACTION_WEB_SEARCH 意图到 Android 意图处理器来在浏览器中打开给定的 URL 。意图处理器通过解析一系列活动，并选择最适合你的意图的一个活动，在这个例子中，是 Web 浏览器活动。意图处理器传递你的网页地址到 Web 浏览器，并打开 Web 浏览器活动。

```java
String q = "https://www.runoob.com";
Intent intent = new Intent(Intent.ACTION_WEB_SEARCH );
intent.putExtra(SearchManager.QUERY, q);
startActivity(intent);
```

上面的例子将在Android搜索引擎上查找"www.runoob.com"，并在一个活动上给出关键词的结果。

对于每一个组件-活动，服务，广播接收器都有独立的机制来传递意图。

| 序号 | 方法和描述                                                   |
| :--- | :----------------------------------------------------------- |
| 1    | Context.startActivity():意图传递给该方法，用于启动一个新的活动或者让已存在的活动做一些新的事情。 |
| 2    | Context.startService():意图传递给该方法，将初始化一个服务，或者新的信息到一个持续存在的服务。 |
| 3    | Context.sendBroadcast():意图传递给该方法，信息将传递到所有对此感兴趣的广播接收器。 |

## 意图对象

意图对象是一包的信息，用于组件接收到的意图就像 Android 系统接受到的信息。

意图对象包括如下的组件，具体取决于要通信或者执行什么。

### 动作(Action)

这是意图对象中必须的部分，被表现为一个字符串。在广播的意图中，动作一旦发生，将会被报告。动作将很大程度上决定意图的其他部分如何被组织。Intent 类定义了一系列动作常量对应不同的意图。这里是一份[Android意图标准动作 ](https://www.runoob.com/android/android-intents-filters.html)列表。

意图对象中的动作可以通过 setAction() 方法来设置，通过 getAction() 方法来读取。

### 数据(Data)

添加数据规格到意图过滤器。这个规格可以只是一个数据类型(如元类型属性)，一条 URI ，或者同时包括数据类型和 URI 。 URI 则由不同部分的属性来指定。

这些指定 URL 格式的属性是可选的，但是也相互独立 -

- 如果意图过滤器没有指定模式，所有其他的 URI 属性将被忽略。
- 如果没有为过滤器指定主机，端口属性和所有路径属性将被忽略。

setData() 方法只能以 URI 来指定数据，setType() 只能以元类型指定数据，setDataAndType() 可以同时指定 URI 和元类型。URI 通过 getData() 读取，类型通过 getType() 读取。

以下是动作/数据组的一些实例 -

| 序号 | 动作/数据组和描述                                            |
| :--- | :----------------------------------------------------------- |
| 1    | ACTION_VIEW content://contacts/people/1：显示ID为1的用户的信息。 |
| 2    | ACTION_DIAL content://contacts/people/1：显示电话拨号器，并填充用户1的数据。 |
| 3    | ACTION_VIEW tel:123：显示电话拨号器，并填充给定的号码。      |
| 4    | ACTION_DIAL tel:123：显示电话拨号器，并填充给定的号码。      |
| 5    | ACTION_EDIT content://contacts/people/1：编辑ID为1的用户信息。 |
| 6    | ACTION_VIEW content://contacts/people/：显示用户列表，以便查看。 |
| 7    | ACTION_SET_WALLPAPER：显示选择壁纸设置。                     |
| 8    | ACTION_SYNC：同步数据，默认的值为：android.intent.action.SYNC |
| 9    | ACTION_SYSTEM_TUTORIAL：开启平台定义的教程（默认教程或者启动教程） |
| 10   | ACTION_TIMEZONE_CHANGED：当时区被改变时通知                  |
| 11   | ACTION_UNINSTALL_PACKAGE：运行默认的卸载器                   |