# 生命周期重要方法

onCreate()

onStart()

onResume()

onPause()

onStop()

onDestroy()

onRestart()

对话框的覆盖和新Activity效果不同，对话框不会导致onPause()和onStop()

但是界面对话框会导致onPause，因为本质是个界面，界面对话框在注册时android：theme = “@style/Theme.AppCompat.Dialog” 不导致onStop()

# Activity的启动

隐式启动系统Activity：

```java
Intent intent = new Intent(Intent.ACTION_VIEW,Uri.parse("https//www.imooc.com"))//参数1action是Activity的别名2Uri
```

隐式启动普通Activity：

```java
Intent intent = new Intent("action",)参数1action是Activity的别名,在声明文件中注册
```

显式启动：

```java
Intent intent = new Intent(this,Main2Activity.class);
```

### startActivityForResult带结果返回的启动

```java
Intent intent = new Intent(this,Main2Activity.class);
startActivityForResult(intent,1000)
需要重写onActivityResult
```

### 传递简单数据

意图的方法

putExtra("aa",1)

getExtra("aa")

### 传递对象

putExtra(String,Serializable) 对象类要实现Serializable接口 把这个类序列化

实例化一个新对象接收Intent.getSerializableExtra(String)

用get方法获取序列的各项内容