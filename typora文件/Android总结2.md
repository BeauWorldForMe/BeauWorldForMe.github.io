+ TakePhotoActivity.java(舌最开始页面)【把type 0 发到下一个Intent】

  ↓

+ RecordVideoActivity【根据selectType进Fragment设置】

  + 设置请求体requestBody
  + 使用post方式发送请求
  + 其中cmlRequestBody是用Android的第三方库OKHTTP上传图片
  + URL在TakePhotoActivity.java的110行读入（在ServerIP.java中设置了网络请求的地址）

+ RecordVideoFragment比较多东西

  + 其中setupFlashModel（）是补光灯的方法接口
  + 其中select（）方法按0、1选择舌面的框是否要出现在屏幕上

+ CorporeityCheckActivity.java其中有语音识别部分的内容
+ PatientInfoQueryResultsMirrorNewActivity.java【体质检测结果】
+ GetAnswerResultBean.java里，变量jiankangzhishu已被更新
+ DynamicWave.java是一个自定义View，是检查结果页面的动态球
+ JianKangFangAnActivity.java 健康方案

