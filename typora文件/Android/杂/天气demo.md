需求

+ 时间、钟表、星期、年月日
+ 类似：

![dc362dd4dae5b1d427965a50898b0cb](C:\Users\15200\AppData\Local\Temp\WeChat Files\dc362dd4dae5b1d427965a50898b0cb.png)



+ 和风天气

https://console.heweather.com/#/console?token=930b49a1723a4e3d9331fb93d323490b

+ 内容（简要）：
  + 显示时间（接口？函数？）
  + 显示天津天气（接口？函数？）

```java
  /**     * 获取系统时间     *     
  * @return     */    
  public static String getDate() {        
  Calendar ca = Calendar.getInstance();        
  int year = ca.get(Calendar.YEAR);           *// 获取年份*        
  int month = ca.get(Calendar.MONTH);         *// 获取月份*        
  int day = ca.get(Calendar.DATE);            *// 获取日*        
  int minute = ca.get(Calendar.MINUTE);       *// 分*        
  int hour = ca.get(Calendar.HOUR);           *// 小时*        
  int second = ca.get(Calendar.SECOND);       *// 秒*         
  String date = "" + year + (month + 1) + day + hour + minute + second;    
  Log.d(TAG, "date:" + date);         return date;    }
```

