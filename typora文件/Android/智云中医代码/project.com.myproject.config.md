```java
/**
 * @Description: 常量配置项
 * @author: wfx
 * @email: wfx19930411@163.com
 * @Date: 2018/3/19 15:09
 */

public class Constants {

    public static String SHAREPREFERENCE_CONFIG_NAME = "anti_collision_settings";   // sp文件名称

    //---------sp存放值的键定义start-------------------------------
    public static final String IS_FIRST_INSTALL = "is_first_install";     // 是否是第一次安装
    public static String CONFIG_USER_INFO = "config_user_info";     // sp中用户信息键值
    public static String CONFIG_USER_MANY_INFO = "config_user_many_info";     // sp中用户详细信息键值
    //---------sp存放值的键定义end---------------------------------


    public static final String TAG = "Safeness";
    public static final int DEBUGLEVEL = AppLog.LEVEL_ALL;        //日志输出级别

    public static final String LogFileDir = "/Safeness";   // 日志文件目录

    /**
     * 接口请求失败错误码
     */
    public static final int RESPONSE_CODE_UNKNOW_HOST = 20001;         // 未知服务器地址
    public static final int RESPONSE_CODE_SOCKET_EXCEPTION = 20002;    // 连接异常
    public static final int RESPONSE_CODE_SOCKET_TIME_OUT = 20003;     // 连接超时
    public static final int RESPONSE_CODE_UNKNOW_ERROR = 20004;        // 未知错误
    public static final int RESPONSE_CODE_GET_RESULT_ERROR = 333333;   // 获取数据时解析出错
    public static final int RESPONSE_SERVER_ERROR = 500;
    public static final int RESPONSE_CODE_Access_denied = 403;   // 拒绝访问
    public static final int RESPONSE_PHONE_ERROR = 400;
    //语音存放位置
    public static final String AUDIO_SAVE_DIR = FileUtil.getDir("audio");
    public static final int DEFAULT_MAX_AUDIO_RECORD_TIME_SECOND = 60;

    public static final int PAGE_SIZE = 10;                              // 分页大小
    public static final String CONFIG_SUCCED_FAILURE= "config_succed_failure";      //配置失败、成功

}
```