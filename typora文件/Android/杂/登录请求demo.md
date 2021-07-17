![f2286c0df3f3b1de5176b2d36342ef7](C:\Users\15200\AppData\Local\Temp\WeChat Files\f2286c0df3f3b1de5176b2d36342ef7.png)

用户名：13672002656

密码：123

URL:https://icloud.tianzhongyimai.com:10082

每次打开一个别人的项目 先用notepad++改动

![image-20200723104814916](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20200723104814916.png)

![image-20200723104825204](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20200723104825204.png)

这两个文件

```java
buildscript {
    
    repositories {
       #配置国内仓库 maven{url'http://maven.aliyun.com/nexus/content/groups/public/'}
        maven{url'http://maven.aliyun.com/nexus/content/repositories/jcenter'}
      google()
      jcenter{url"http://jcenter.bintray.com/"}
      maven{url"https://jitpack.io"}
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.4.1' #修改为自己的android版本
        

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        maven{url'http://maven.aliyun.com/nexus/content/groups/public/'}
        maven{url'http://maven.aliyun.com/nexus/content/repositories/jcenter'}
      google()
      jcenter{url"http://jcenter.bintray.com/"}
      maven{url"https://jitpack.io"}
    }
}
```

```java
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
distributionUrl=https\://services.gradle.org/distributions/gradle-5.1.1-all.zip  #本地gradle版本
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
```



 POST方式请求登录:由于post方式是直接通过流的方式向服务器端写数据，所以步骤要多一些:
      

```
  1、设置请求路径字符串(不带请求参数)
            String path = "http://192.168.1.10/login/LoginServlet";

        2、包装请求 url
            URL url = new URL(path);
        
        3、创建连接
            HttpURLConnection conn = (HttpURLConnection)ur.openConnection();
        
        4、设置连接方式和连接超时时长
            conn.setRequestMethod("POST");
            conn.setConnectionTimeout(5000);
        
        5、准备好要发送的数据
            String data = "name="+URLEncoder.encode(name)+"password="+URLEncoder.encode(password);
    
        6、设置GET另外需要的请求头 Content-Type和Content-Length
            
            conn.setRequestProperty("Content-Type","application/x-www-form-urlencoded");            
            conn.setRequestProperty("Conent-Length",data.length()+"");
    
        7、告诉URLConnection是输入还是输出
            URL 连接可用于输入和/或输出。
            如果打算使用 URL 连接进行输出，则将 DoOutput 标志设置为 true;如果不打算使用，则设置为                     
           false。默认值为 false;
            如果打算使用 URL 连接进行输入，则将 DoInput 标志设置为 true; 如果不打算使用，则设置为                    
           false。默认值为 true。
            conn.setDoOutput(true);
        
        8、创建conn的输出流
            OutputStream os = conn.getOutputStream();
            
        9、输出内容
            os.write(data.getBytes());
        
        10、接收请求响应码和响应数据
            if(conn.getResponseCode==200){
                InputStream is = conn.getInputStream();
                byte [] data = StreamTools.getBytes(is);  
                /*StreamTools是一个工具类,将输入流中的数据存放到字节缓冲数组ByteArrayStream中，
                  这个数组的长度可以动太改变，因为如果直接用数组存，不知道要new 一个多大的数组，
                  直接声明的时候就给数组赋值，就不用指定数组的长度。
                */
                String result = new String(data);
            }


```

# 界面

 RelativeLayout 相对布局:使用相对布局，在容器中的子元素可以使用彼此之间的相对位置或者与容器之间的相对位置进行定位.

1.下面是实现登陆效果的截图：



2.布局文件要使用到的字符资源文件strings.xml


<?xml version="1.0" encoding="utf-8"?>
<resources>

    <string name="app_name">lesson03</string>
    <string name="hello_world">Hello world!</string>
    
    <string name="user_name">用户名</string>
    <string name="user_pass">密    码</string>
    <string name="user_login">登陆</string>
    <string name="user_rem">记住密码</string>
    <string name="tip_name">请输入用户名</string>
    <string name="tip_pass">请输入用户密码</string>
    <string name="tip_result">服务器返回的数据</string>

</resources>
3.layout布局文件(相应属性的说明见注释)activity_login.xml

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="${packageName}.${activityClass}" >

    <TextView
        android:id="@+id/tv_name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="20sp"
        android:layout_alignBaseline="@+id/et_name"
        android:text="@string/user_name" />
    <!-- 
      android:textSize="20sp"  设置字体大小
      android:layout_alignBaseline="@+id/et_name" 让TextView与id=et_name的控件在同水平线上(同一行上)
     -->
    
    <EditText
        android:id="@+id/et_name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_toRightOf="@+id/tv_name"
        android:hint="@string/tip_name" />
    <!-- 
    android:layout_alignParentRight="true" 子控件针对父容器 右端对齐
    android:layout_toRightOf:在控件tv_name的右侧
     -->


​    
   <TextView
​        android:id="@+id/tv_pass"
​        android:layout_width="wrap_content"
​        android:layout_height="wrap_content"
​        android:layout_alignBaseline="@+id/et_pass"
​        android:layout_below="@+id/tv_name"
​        android:textSize="20sp"
​        android:text="@string/user_pass" />
   <!-- 

      android:layout_below="@+id/tv_name" :位于tv_name控件的下方
    -->
    
    <EditText
        android:id="@+id/et_pass"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentRight="true"
        android:layout_toRightOf="@+id/tv_pass"
        android:layout_below="@+id/et_name"
        android:hint="@string/tip_name" />


​    
​    <Button 
​        android:id="@+id/btn_login"
​        android:layout_width="wrap_content"
​        android:layout_height="wrap_content"
​        android:layout_marginTop="30dp"
​        android:layout_below="@+id/tv_pass"
​        android:onClick="login"
​        android:text="@string/user_login"/>
​    
    <!-- 
       android:layout_marginTop="30dp":该控件的上边距的为30dp大小
     -->
    <CheckBox 
        android:id="@+id/chbx_rem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignBaseline="@+id/btn_login"
        android:layout_marginLeft="50dp"
        android:layout_below="@+id/et_pass"
        android:layout_toRightOf="@+id/btn_login"
        android:text="@string/user_rem"/>
    <!-- 
         android:layout_marginLeft="50dp":该控件的左边距为50dp大小
     -->
     
    <TextView 
        android:id="@+id/tv_result"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:text="@string/tip_result"/>
    <!-- 
        android:layout_alignParentBottom="true" :子控件针对父容器 底端对齐
     -->

</RelativeLayout>
4.在相对布局中还有一些属性比如：

android:layout_centerInparent = "true" ，表示该控件在父控件容器的水平与垂直方向居中 

等等.....希望自己下去多多研究!

5.自己部署查看运行结果.

# 网络相关

1.概述

        每个 HttpURLConnection 实例都可用于生成单个请求，但是其他实例可以透明地共享连接到 HTTP 服务器的基础网络。请求后在 HttpURLConnection 的 InputStream 或 OutputStream 上调用 close() 方法可以释放与此实例关联的网络资源，但对共享的持久连接没有任何影响。如果在调用 disconnect() 时持久连接空闲，则可能关闭基础套接字。

2.在03_android入门_采用RelativeLayout实现登陆界面效果的案例继续完善 效果如下：

 

点击登陆按钮 在服务器的控制台看到的结果



在点击登陆按钮之前，先通过eclipse中所带的LogCat的工具，点击



+号 弹出对话框



添加过滤的名称和过滤的标识 点击ok完成。

当点击登陆按钮之后即可在LogCat中看到执行的结果



当你输入错误的用户名和密码的时候你可以看到如下效果



3.具体LoginActivity代码的实现如下：(备注：在代码中我添加了详细的注释请仔细阅读)

package www.csdn.net.lesson03;

import java.io.ByteArrayOutputStream;
import java.io.InputStream;

import java.net.HttpURLConnection;
import java.net.URL;
import java.net.URLEncoder;

import android.app.Activity;
import android.os.Bundle;
import android.text.TextUtils;
import android.view.View;
import android.widget.EditText;
import android.widget.Toast;

public class LoginActivity extends Activity {

	// 声明控件对象
	private EditText et_name, et_pass;
	 
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		// 设置显示的视图
		setContentView(R.layout.activity_login);
		// 通过 findViewById(id)方法获取用户名的控件对象
		et_name = (EditText) findViewById(R.id.et_name);
		// 通过 findViewById(id)方法获取用户密码的控件对象
		et_pass = (EditText) findViewById(R.id.et_pass);
	 
	}
	 
	/**
	 * 通过android:onClick="login"指定的方法 ， 要求这个方法中接受你点击控件对象的参数v
	 * 
	 * @param v
	 */
	public void login(View v) {
		// 获取点击控件的id
		int id = v.getId();
		// 根据id进行判断进行怎么样的处理
		switch (id) {
		// 登陆事件的处理
		case R.id.btn_login:
			// 获取用户名
			final String userName = et_name.getText().toString();
			// 获取用户密码
			final String userPass = et_pass.getText().toString();
			if (TextUtils.isEmpty(userName) || TextUtils.isEmpty(userPass)) {
				Toast.makeText(this, "用户名或者密码不能为空", Toast.LENGTH_LONG).show();
			} else {
				System.out
						.println("----------------------发送请求到服务器----------------------");
				// <span style="color:#ff6666;">访问网络 （需要一个网络的权限） <uses-permission
				// android:name="android.permission.INTERNET"/></span>
				// <span style="color:#ff6666;">访问网络(耗时的操作) 避免阻塞主线程(UI) 需要开启新的子线程来处理</span>
				new Thread() {
					public void run() {
						// 调用loginByGet方法
						loginByGet(userName, userPass);
	 
					};
				}.start();
			}
	 
			break;
	 
		default:
			break;
		}
	 
	}
	 
	/**
	 * 通过GET方式发送的请求
	 * 
	 * @param userName
	 * @param userPass
	 */
	public void loginByGet(String userName, String userPass) {
	 
		try {
			// 设置请求的地址 通过URLEncoder.encode(String s, String enc)
			// 使用指定的编码机制将字符串转换为 application/x-www-form-urlencoded 格式
			String spec = "<span style="color:#ff6666;">http://172.16.237.200:8080/video/login.do</span>?username="
					+ URLEncoder.encode(userName, "UTF-8") + "&userpass="
					+ URLEncoder.encode(userPass, "UTF-8");
			// 根据地址创建URL对象(网络访问的url)
			URL url = new URL(spec);
			// url.openConnection()打开网络链接
			HttpURLConnection urlConnection = (HttpURLConnection) url
					.openConnection();
			urlConnection.setRequestMethod("GET");// 设置请求的方式
			urlConnection.setReadTimeout(5000);// 设置超时的时间
			urlConnection.setConnectTimeout(5000);// 设置链接超时的时间
			// 设置请求的头
			urlConnection
					.setRequestProperty("User-Agent",
							"Mozilla/5.0 (Windows NT 6.3; WOW64; rv:27.0) Gecko/20100101 Firefox/27.0");
			// 获取响应的状态码 404 200 505 302
			if (urlConnection.getResponseCode() == 200) {
				// 获取响应的输入流对象
				InputStream is = urlConnection.getInputStream();
	 
				// 创建字节输出流对象
				ByteArrayOutputStream os = new ByteArrayOutputStream();
				// 定义读取的长度
				int len = 0;
				// 定义缓冲区
				byte buffer[] = new byte[1024];
				// 按照缓冲区的大小，循环读取
				while ((len = is.read(buffer)) != -1) {
					// 根据读取的长度写入到os对象中
					os.write(buffer, 0, len);
				}
				// 释放资源
				is.close();
				os.close();
				// 返回字符串
				String result = new String(os.toByteArray());
				System.out.println("***************" + result
						+ "******************");
			} else {
				System.out.println("------------------链接失败-----------------");
			}
	 
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}

4.项目清单文件(AndroidManifest.xml)
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="www.csdn.net.lesson03"
    android:versionCode="1"
    android:versionName="1.0" >

    <uses-sdk
        android:minSdkVersion="14"
        android:targetSdkVersion="19" />
    <!-- 添加访问网络的权限 -->
    <uses-permission android:name="android.permission.INTERNET"/>
     
    <application
        android:allowBackup="true"
        android:icon="@drawable/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >
        <activity
            android:name="www.csdn.net.lesson03.LoginActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>

5.关于服务器中我仅写一个Servlet进行处理相应的请求处理


package www.csdn.net.servlet;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class LoginServlet extends HttpServlet {

	/**
	 * 
	 */
	private static final long serialVersionUID = 1L;
	 
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		//获取请求的参数值
		String userName = request.getParameter("username");
		String userPass = request.getParameter("userpass");
		
		System.out.println("在没有转码之前的"+userName+"---"+userPass);
		//GET方式的请求乱码处理
		userName = new String(userName.getBytes("ISO8859-1"),"UTF-8");
		userPass = new String(userPass.getBytes("ISO8859-1"),"UTF-8");
	 
		System.out.println("在转码之后---"+userName+"---"+userPass);
		if("陈红军".equals(userName)&&"123".equals(userPass)){
			//响应登陆成功的信息
			response.getOutputStream().write("登陆成功".getBytes()); 
		}else{
			//相应登陆失败的信息
			response.getOutputStream().write("登陆失败".getBytes());
		}
		
	}
	 
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		this.doGet(request, response);
	}

}
对应的web.xml文件的配置是：
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" id="WebApp_ID" version="2.5">
  <display-name>video</display-name>

  <servlet>
    <description></description>
    <display-name>LoginServlet</display-name>
    <servlet-name>LoginServlet</servlet-name>
    <servlet-class>www.csdn.net.servlet.LoginServlet</servlet-class>
  </servlet>

  <servlet-mapping>
    <servlet-name>LoginServlet</servlet-name>
    <url-pattern>/login.do</url-pattern>
  </servlet-mapping>

</web-app>

6.关于程序中学生经常出现的bug分析
  6.1.忘记在项目清单文件中添加访问网络的权限.

  <!-- 添加访问网络的权限 -->
    <uses-permission android:name="android.permission.INTERNET"/>
    那么程序运行的时候会出现如下bug


6.2.在按钮点击的事件处理中直接调用

loginByGet(userName, userPass);
方法没有在子线程中调用
loginByGet(userName, userPass);
方法 就会出现如下bug


bug说明：在android4.0以后的版本中要想发送一个网络的请求，就必须把这个请求写在子线程中，否则就会出现如上的bug

6.3.在发送网路的请求的时候把请求的地址：

http://172.16.237.200:8080/video/login.do
写成了
http://localhost:8080/video/login.do或者http://127.0.0.1:8080/video/login.do

就会出现如下bug:





以上理解之后请同学们思考怎么把返回的数据写在下图的位置尼







虚拟机访问本地网络10.0.2.2：端口/get/text