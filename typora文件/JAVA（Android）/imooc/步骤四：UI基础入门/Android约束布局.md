# ConstraintLayout约束布局

帧布局FrameLayout了解：

+ 有一个z轴 方向向里
+ 重要属性：重力、前景、前景重力

表格布局TableLayout了解：

+ 如果直接往TableLayout添加控件，默认和屏幕等宽，如果想使多个控件在同一行需要在这些控件外层包裹TableRow

+ android：syretchColumns拉长哪一列
+ android：shrinkColumns缩短某一列
+ android：collapseColumns设置可以隐藏的列
+ android:layout_span跨列

网格布局GridLayout了解：

+ android:columnCount列数量
+ android:layout_columnSpan跨几列
+ android:layout_columnWeight列权重
+ 对应的还有row

## 约束布局

属性：

+ app:layout_constraintBottom_toBottomOf约束当前view的底部位置

+ app:layout_constraintVertical_bias垂直偏移量

很好用的布局，两大优势

+ 可视化编程
+ 



# CheckBox

系统封装的复选控件

+ setChecked（false）设置状态

+ isChecked = checkBox.isChecked() 获取状态

+ ```java
   setOnCheckedChangeListener（new CompoundButton.OnCheckedChangeListener(){
   
   }）
  ```

# RadioButton

单选控件

可以和RadioGroup一起使用，只能选择一个

通过点击无法变为未选中，一组RadioButton只能同时选中一个

默认圆形

# ToggleButton

切换程序中的状态

两种状态

+ android：textOn

+ android：textOff

+ android：setChecked（boolean）

+ ```java
   setOnCheckedChangeListener（new CompoundButton.OnCheckedChangeListener(){
   
   }）
  ```

# SeekBar

搜寻显示当前进度的控件

android:max

android:progress

setMax

setProgress

setOnSeekBarChangeListener()