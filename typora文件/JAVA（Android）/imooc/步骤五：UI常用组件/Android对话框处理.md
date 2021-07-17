+ 提示对话框AlertDialog

  + 向用户传递提示或警告

  + setTitle

  + setMessage

  + create

  + show

  + 步骤：

    + 实例化一个builder
    + 设置标题、文本等样式
    + 设置几个按钮（有的需要点击事件）
    + 调用show方法

    ```java
    public void myClick(View view){
            switch (view.getId()){
                case R.id.normal_dialog_btn:
                    AlertDialog.Builder builder = new AlertDialog.Builder(this);
                    builder.setTitle("提示");
                    builder.setMessage("确定退出吗？");
                    builder.setPositiveButton("确定", new DialogInterface.OnClickListener() {
                        @Override
                        public void onClick(DialogInterface dialogInterface, int i) {
                            finish();
                        }
                    });
                    builder.setNegativeButton("取消",null);
                    builder.show();
                    break;
                case R.id.diy_dialog_btn:
                    break;
            }
        }
    ```

    

+ 自定义Dialog

  + 设置布局、style、自定义Dialog、显示
  + 步骤
    + 设计自定义对话框样式（按钮背景等）-->dialog_layout.xml
    + 设计style（去标题栏、去背景）-->res.styles.xml
    + 将第一步的布局应用到当前自定义对话框
    + 实例化对话框（参数1，环境上下文，参数二，第二步创建的styles R.styles.mydialog）
    + 并展示show()

+ PopupWindow弹窗

  + 需要的时候给更多选择，平时不出现

  + 步骤：

    + 准备弹窗所需要的视图对象

      + ```jiava
        View v = LayoutInflater.from(this).inflate(R.layout.popup_layout,null)
        ```

    + 创建PopupWindow对象实例

      + 参数1：用在弹窗的View 参数2、3：弹窗的宽高 参数4focuable:能否获取焦点

      + ```java
        PopupWindow window = new PopupWindow(v,200,40,true)
        ```

    + 设置背景、注册事件监听器和添加动画

      + ```
        window.setBackgroundDrawable(new ColorDrawable(Color.TRANSPARENT));//背景
        window.setOutsideTouchable(true);//设置能响应外部的点击事件
        window.setTouchable(true)//设置能响应点击事件
        ```

    + 显示PopupWindow

      + 参数1（anchor）锚 参数2、3:相对于锚在xy的偏移量

      + ```
        window.showAsDropDown(view)
        ```

    + 为弹窗中文本添加点击事件

      + ```java
        v.findViewById(R.id.choose).setOnClickListener(new View.OnClickListener(){
        	@Override
        	public void onClick(View view){
        		Toast.makeText(MainActivity.this,"你点了选择"，Toast.LENGTH_SHORT).show();
        		window.dismiss()
        	}
        })
        ```

    + 动画

      + 创建一个动画资源res--anim--translate.xml
        + translate移动动画
          + from、to属性
          + duration持续时间属性
        + alpha透明动画
        + rotate旋转动画
        + scale缩放动画
      + 创建一个style应用动画资源
      + 将window.setAnimationStyle(R.style.xxx)设置好

+ # ArrayAdapter对话框进阶

  + 数组适配器 只能用来显示单一的文本
  + 构造方法，参数：1环境 2布局资源索引大 3布局中textView的id 4数据源

```java
ArrayAdapter adapter = new ArrayAdapter(this,R.layout.array_item_layout,R.id.item_txt,items);
```

```java
AlertDialog.Builder builder = new AlertDialog.Builder(this).setTitle("请选择").setAdapter(adapter,new DialogInterface.OnClickListener(){
	@Override
	public void onClick(View view){
		Toast.makeText(MainActivity.this,items[i],LENGTH_LONG).show();
	}
})//参数1适配器对象2监听器
```

