# Android 概述

## 什么是 Android？

![android_overview_1](https://www.runoob.com/wp-content/uploads/2015/05/android_overview_1.jpg)



Android 是一个开源的，基于 Linux 的移动设备操作系统，如智能手机和平板电脑。Android 是由谷歌及其他公司带领的开放手机联盟开发的。



Android 提供了一个统一的应用程序开发方法，这意味着开发人员只需要为 Android 进行开发，这样他们的应用程序就能够运行在不同搭载 Android 的移动设备上。

谷歌在2007年发布了第一个测试版本的 Android 软件开发工具包（SDK），第一个商业版本的 Android 1.0，则发布于2008年9月。

2012年6月27日，在谷歌I/O大会上，谷歌宣布发布了 Android 版本4.1 Jelly Bean。 Jelly Bean 是一个在功能和性能方面的渐进的更新，主要目的是改进用户界面，

Android 源代码是根据自由和开放源码软件许可证。谷歌发布的大部分代码遵循 Apache 许可证2.0版，Linux 内核的变化遵循 GNU 通用公共许可证版本2。

------

## Android 开发优势

- 开放源代码
- 众多开发者及强大的社区
- 不断增长的市场
- 国际化的 App 集成
- 低廉的开发成本
- 更高的成功几率
- 丰富的开发环境

![img](https://www.runoob.com/wp-content/uploads/2015/05/why_android.jpg)

## Android 的特性

Android 是一款与 Apple 4GS 竞争的功能强大的操作系统，并支持一些伟大的特性。以下列举出部分功能：

| 特性             | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| 漂亮的 UI        | Android 操作系统的基本屏幕提供了漂亮又直观的用户界面。       |
| 连接性           | GSM/EDGE, IDEN, CDMA, EV-DO, UMTS, Bluetooth, Wi-Fi, LTE, NFC 和 WiMAX. |
| 存储             | 用于数据存储的轻量级关系型数据库SQLite                       |
| 媒体支持         | H.263, H.264, MPEG-4 SP, AMR, AMR-WB, AAC, HE-AAC, AAC 5.1, MP3, MIDI, Ogg Vorbis, WAV, JPEG, PNG, GIF, 和 BMP |
| 消息             | SMS 和 MMS                                                   |
| Web 浏览器       | 基于开源的 WebKit 布局引擎，再加上支持 HTML5 和 CSS3 Chrome 的 V8 JavaScript 引擎。 |
| 多点触控         | Android原生支持多点触控，从最初的手持设备开始便有，如 HTC Hero。 |
| 多任务           | 用户可以跳从一个任务到另一个任务，并且相同时间可以同时运行各种应用。 |
| 可调整的 widgets | Widgets是可调整大小，这样用户就可以扩大更多的内容或缩小以节省空间。 |
| 多语言           | 支持单向和多向文本。                                         |
| GCM              | 谷歌云消息（GCM）是一种服务，让开发人员对 Android 设备的用户发送短消息数据，而无需专有的同步解决方案。 |
| Wi-Fi Direct     | 一种通过高带宽的对等网络连接来直接发现和配对应用的技术。     |
| Android Beam     | 一个流行的基于 NFC 的技术，使用户能够即时共享，只需通过触摸 NFC 功能将两个手机连在一起。 |

------

## Android 应用程序

Android 应用程序一般使用 Android 软件开发工具包，采用 Java 语言来开发。

一旦开发完成，Android 应用程序可以容易的打包，并在诸如 Google Play 和亚马逊应用商店上出售。

Android 在世界各地190多个国家有数以百万计的移动设备。这是任何移动平台和快速增长的最大的安装基础。全球每天有超过100万个新的 Android 设备被激活。

本教程的写作目的是教会你如何开发并打包 Android 应用程序。我们将从 Android 应用程序编程环境设置开始，然后深入 Android 应用程序开发的各个方面。

## Android 应用程序的类别

市场上有许多 Android 应用。主要类别有：

![image](https://www.runoob.com/wp-content/uploads/2015/05/android_overview_3.png)

## Android 的历史

Android 的代码名称现在从 A 排到了 L，分别是 Aestro, Blender, Cupcake, Donut, Eclair, Froyo, Gingerbread, Honeycomb, Ice Cream Sandwitch, Jelly Bean, KitKat and Lollipop。让我们按顺序了解 Android 的历史。

- 纸杯蛋糕 (Cupcake)
- 甜甜圈 (Donut)
- 闪电泡芙 (Eclair)
- 冻酸奶 (Froyo)
- 姜饼 (Gingerbread)
- 蜂巢 (Honeycomb)
- 冰淇淋三明治 (Ice Cream Sandwich)
- 果冻豆 (Jelly Bean)
- 奇巧 (KitKat)
- 棒棒糖 (Lollipop)



![img](https://www.runoob.com/wp-content/uploads/2015/05/jistory.jpg)

------

## 什么是 API 级别？

API 级别是一个用于唯一标识 API 框架版本的整数，由某个版本的 Android 平台提供。

| 平台版本                              | API 等级 | VERSION_CODE           |                           |
| :------------------------------------ | :------- | :--------------------- | :------------------------ |
| Android 5.1                           | 22       | LOLLIPOP_MR1           |                           |
| Android 5.0                           | 21       | LOLLIPOP               |                           |
| Android 4.4W                          | 20       | KITKAT_WATCH           | KitKat for Wearables Only |
| Android 4.4                           | 19       | KITKAT                 |                           |
| Android 4.3                           | 18       | JELLY_BEAN_MR2         |                           |
| Android 4.2, 4.2.2                    | 17       | JELLY_BEAN_MR1         |                           |
| Android 4.1, 4.1.1                    | 16       | JELLY_BEAN             |                           |
| Android 4.0.3, 4.0.4                  | 15       | ICE_CREAM_SANDWICH_MR1 |                           |
| Android 4.0, 4.0.1, 4.0.2             | 14       | ICE_CREAM_SANDWICH     |                           |
| Android 3.2                           | 13       | HONEYCOMB_MR2          |                           |
| Android 3.1.x                         | 12       | HONEYCOMB_MR1          |                           |
| Android 3.0.x                         | 11       | HONEYCOMB              |                           |
| Android 2.3.4Android 2.3.3            | 10       | GINGERBREAD_MR1        |                           |
| Android 2.3.2Android 2.3.1Android 2.3 | 9        | GINGERBREAD            |                           |
| Android 2.2.x                         | 8        | FROYO                  |                           |
| Android 2.1.x                         | 7        | ECLAIR_MR1             |                           |
| Android 2.0.1                         | 6        | ECLAIR_0_1             |                           |
| Android 2.0                           | 5        | ECLAIR                 |                           |
| Android 1.6                           | 4        | DONUT                  |                           |
| Android 1.5                           | 3        | CUPCAKE                |                           |
| Android 1.1                           | 2        | BASE_1_1               |                           |
| Android 1.0                           | 1        | BASE                   |                           |