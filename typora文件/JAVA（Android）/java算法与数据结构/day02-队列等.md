## 队列

+ 有序列表，可以用数组或链表

+ 遵循先入先出原则

### 数组模拟队列

maxSize该队列最大容量

需要两个变量front和rear分别记录队列前后端的下标，front会随着数据输出而改变，rear会随着数据输入而改变

![image-20210609110414423](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210609110414423.png)





优化：环形队列

front变：指向队列第一个元素

rear变：指向队列最后一个元素后一个位置

