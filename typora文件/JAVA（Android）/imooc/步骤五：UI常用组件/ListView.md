+ ArrayAdapter步骤：
  + 在布局文件中加一个ListView
  + ArrayAdapter（环境，布局textView，数据源（数组））
    + 这里第二个参数可以使用Android自带的资源android.R.layout.simple_list_item_1 
  + setAdapter()
+ SimpleAdapter步骤（这个可以加图片排版 ）：
  + 在布局文件中加一个ListView
  + SimpleAdapter（环境，数据源（数组）,布局textView，from数据来源map的key数组,to数据去向的id数组）
    + 这里第二个参数可以使用Android自带的资源android.R.layout.simple_list_item_1 
  + setAdapter()
+ BaseAdapter：
  + 在布局文件中加一个ListView
  + 写一个MyAdapter继承BaseAdapter
  + new一个MyAdapter
  + 准备数据源（每项的布局）
  + 设置适配器setAdapter()

# ViewHolder 优化

view为null时，完成对ViewHolder的实例化，为各个控件属性赋值

view.setTag(holder)

else: holder = (ViewHolder)view.getTag();







