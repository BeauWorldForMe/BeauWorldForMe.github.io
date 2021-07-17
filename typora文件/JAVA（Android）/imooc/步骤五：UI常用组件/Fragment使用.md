Fragment不能脱离Activity存在

一个Activity可以运行多个Fragment

# Fragment的加载

+ 静态加载
  
  + 通过android：name属性指定fragment路径
  
    + ```
      android:name="com.example.fragmentdemo.Fragment1"
      ```
+ 动态加载

  + 设置FrameLayout帧布局，留一个空间

  + 创建Fragment

  + 在Activity里加进来Fragment

    + 获取FragmentManager管理器

      ```
      FragmentManager manager = getSupportFragmentManager();
      ```

    + 获取FragmentTransaction事务（开启事务）

      ```
      FragmentTransaction transaction = manager.beginTransaction();
      ```

    +  动态添加Fragment 参数1容器id 参数2Fragment对象

       ```
       transaction.add(R.id.container,new Fragment())
       ```

    +  提交事务

       ```
       transaction.commit()
       ```

       

## selector选择器，根据控件不同状态选择资源控制显示效果

drawable右键--new一个drawable对象



## 传值

Activity向Fragment

+ setArguments

+ ```java
  //setArguements
                  //1.实例化Fragment
                  Fragment f1 = new ChannelFragment();
                  //2.实例化一个Bundle对象（载体）
                  Bundle bundle = new Bundle();
                  //3.存入数据到Bundle对象中
                  bundle.putString("msg1","这是由Activity发往Fragment的数据");
                  //4.调用Fragment的setArguments方法，传入Bundle对象
                  f1.setArguments(bundle);
                  //5.添加/替换显示的Fragment
                  transaction.replace(R.id.container,f1);
  ```

  

Fragment向Activity

+ Callback

+ 步骤：

  + 自己定义一个回调接口，在该接口中声明一个用于传递数据的方法

    ```java
    public interface MyListener(){
    	public void sendMsg(String msg);
    }
    ```

  + 让Activity实现该接口，然后重写这个回调方法，获取传入的值，然后做处理

  + 在自定义Fragment中，声明一个回调接口的引用

  + 在onAttach中，为第三步的引用赋值（这个值会传回去）

    ```java
    m1=(MyListener)getActivity();
    m1.sendMsg("消息")
    ```

    

  