+ 无法预测存储数据数量的时候，用集合
+ 同时存储具有一对一关系的数据
+ 需要进行数据的增删
+ 数据重复问题

![image-20210510125300351](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210510125300351.png)



## List概述

+ 元素有序并且可以重复，称为序列
+ 可以精确控制元素插入位置，或删除某个位置元素
+ 两个主要实现类 ArrayList和LinkedList

## ArrayList

+ 底层由数组实现
+ 动态增长，以满足应用程序需求
+ 在列表尾部插入和删除数据非常有效
+ 更适合查找和更新元素
+ 元素可以为null
+ 常用方法
  + add()
  + size（）
  + get(index)
  + sort（）
  + remove()
  + contains()
  + set(index,内容)

## Set

+ 无序、不可重复

+ 重点HashSet

  ## HashSet哈希集

  + 只允许一个null元素
  + 具有良好的存取和查找性能
  + 常用方法
    + 构造：Set set = new HashSet()
    + set.add() 添加元素 
    + Iterator it = set.iterator()；创建迭代器
    + while(it.hasNext()){System.out.print(it.next()+ " ")}遍历迭代器
    + toString()
    + 重写hashCode()和equals判断两个对象是否相对 
    + contains()是否包含对象
    + next()得到一个Object类型，有时要强制转换成对象类型
    + isEmpty()
    + removeAll（set）移除一个子集
  + 泛型<> 引入之后去掉了强制类型转换的过程

## Map

+ 数据以键值对存储key value

+ 可以通过key快速查找到value

+ key值唯一

  ## HashMap

  + 基于哈希表的Map接口实现
  + 允许使用null值和null键
  + key值唯一
  + 其中额Entry对象是无序排列的
  + Interface Map<K,V>
    + clear()清空Map
    + entrySet()返回所有信息
    + keySet()取出所有key
    + put(K,V)
    + values()得到value
    + get(key)通过key得到value

  ```java
  public class DictionaryDemo {
  
  	public static void main(String[] args) {
  		// TODO Auto-generated method stub
  		Map<String,String> map = new HashMap<String,String>();
  		System.out.println("请输入三组单词对应的注释，并存放到HashMap中");
  		Scanner in = new Scanner(System.in);
  		int i = 0;
  		while(i<3) {
  			System.out.println("请输入key值（单词）：");
  			String key = in.next();
  			System.out.println("请输入value值（注释）：");
  			String value = in.next();
  			map.put(key, value);
  			i++;
  		}
  		System.out.println("========================================");
  		//打印，直接使用迭代器输出所有value
  		System.out.println("使用迭代器输出所有value");
  		Iterator<String> it = map.values().iterator(); 
  		while(it.hasNext()) {
  			System.out.println(it.next()+" ");
  		}
  		//打印key和value，通过entrySet()
  		System.out.println("========================================");
  		System.out.println("通过entrySet打印key和value");
  		Set<Entry<String,String>> entrySet = map.entrySet();
  		for(Entry<String,String> entry:entrySet) {
  			System.out.println(entry.getKey()+"----"+entry.getValue());
  		}	
  	}
  }
  ```

  + 查找字典中数据

    + keySet的方法

    + get(key)

    + contains(key)是否包含这个key值

      