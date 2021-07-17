## 链表

+ 有序列表

+ 存储时，有节点存放（每个节点包含data域和next域）
+ 链式存储，各个节点不一定连续存放
+ 分为带头节点的链表和不带头节点的链表
  + 带头节点head--null 

![image-20210617162455914](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210617162455914.png)

增删改查

![image-20210617170424697](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210617170424697.png)





栈数据结构 ：先进后出

push进去  pop弹出

![image-20210621172123944](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210621172123944.png)

![image-20210621174404032](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210621174404032.png)

双向链表多了一个pre属性

单向环形链表-约瑟夫问题

```java
package circleLinkedList;

public class Josepfu {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		//测试一把
		int n=125;//n人
		int m=20;
		int k=10;//从k开始
		CircleSingleLinkedList circleSingleLinkedList = new CircleSingleLinkedList();
		circleSingleLinkedList.addBoy(n);
		circleSingleLinkedList.showBoy();
		circleSingleLinkedList.showJosepfu(k,m,n);

	}

}

//创建一个环形单向链表
class CircleSingleLinkedList{
	//创建一个first节点，当前没编号
	private Boy first = new Boy(-1);
	//添加小孩节点，构成环形链表
	public void addBoy(int nums) {
		//nums做一个数据校验
		if(nums<1) {
			System.out.println("nums的值不正确");
			return;
		}
		Boy curBoy = null;//辅助指针，帮助构建环形链表
		//使用for来创建我们的环形链表
		for(int i=1;i<=nums;i++) {
			//根据编号，创建小孩节点
			Boy boy = new Boy(i);
			if(i==1) {
				first = boy;
				first.setNext(first);//构成环
				curBoy = first;//让curBoy指向第一个小孩
			}else {
				curBoy.setNext(boy);
				boy.setNext(first);
				curBoy = boy;
			}
		}
	}
	
	//遍历当前链表
	public void showBoy() {
		//判断是否为空
		if(first == null) {
			System.out.println("链表空");
			return;
		}
		Boy curBoy = first;
		while(true) {
			System.out.printf("小孩的编号%d\n",curBoy.getNo());
			if(curBoy.getNext()==first) {
				break;//遍历完毕了
			}
			curBoy = curBoy.getNext();
		}
		
	}
	
	//解决约瑟夫问题,数m的人出列
	public void showJosepfu(int startNo,int m,int n) {
		//判断是否为空
		if(first == null||startNo<1||startNo>n) {
			System.out.println("链表空");
			return;
		}
		Boy helper = null; //创建一个辅助变量，事先指向环形最后
		//先找到最后一个
		Boy curBoy = first;
		while(true) {
			if(curBoy.getNext()==first) {
				helper = curBoy;
				break;//遍历完毕了
			}
			curBoy = curBoy.getNext();
		}
		//在报数前，先让helper和first都移动到startNo位置，即startNo-1次
		for(int i=1;i<startNo;i++) {
			helper=helper.getNext();
			first=first.getNext();
		}
		while(true) {
			if(helper == first) {
				//这时只有1个节点
				break;
			}
			for(int i=1;i<m;i++) {
				helper=helper.getNext();
				first=first.getNext();
			}
			//first指向的人出列
			System.out.printf("出列的人是%d号\n",first.getNo());
			first = first.getNext();
			helper.setNext(first);
		}
		System.out.printf("最后留下是%d号\n",first.getNo());
		
	}
}

//创建一个Boy类，表示一个节点
class Boy{
	private int no;
	private Boy next;
	public Boy(int no) {
		this.no = no;
	}
	public int getNo() {
		return no;
	}
	public void setNo(int no) {
		this.no = no;
	}
	public Boy getNext() {
		return next;
	}
	public void setNext(Boy next) {
		this.next = next;
	}
	
}
```

