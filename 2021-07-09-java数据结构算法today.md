## 赫夫曼树结构

![image-20210709135655552](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210709135655552.png)



wpl最小的二叉树就是赫夫曼树

![image-20210709140852414](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210709140852414.png)

```java
package com.tree;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class HuffmanTree {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int[] arr = {13,7,8,3,29,6,1};
		Node root = createHuffmanTree(arr);
		
		//测试一把
		preOrder(root);
	}
	
	//写一个前序遍历的方法用来测试
	public static void preOrder(Node root) {
		if(root!=null) {
			root.preOrder();
		}else {
			System.out.println("空树不能遍历");
		}
	}
	//创建赫夫曼树的方法
	public static Node createHuffmanTree(int[] arr) {
		//第一步，为了操作方便
		//1.遍历arr
		//2.将arr每个元素构建成一个Node
		//3.将Node放入到ArrayList中
		List<Node> nodes = new ArrayList<Node>();
		for(int value:arr) {
			nodes.add(new Node(value));
		}
		
		while(nodes.size()>1) {
			//排序 从小到大
			Collections.sort(nodes);
			System.out.println("nodes =" +nodes);
			//取出根节点权值最小的两棵二叉树
			//1.取出最小的节点
			Node leftNode = nodes.get(0);
			//2.取出第二小的节点
			Node rightNode = nodes.get(1);
			//3.构建一颗新的二叉树
			Node parent = new Node(leftNode.value + rightNode.value);
			parent.left = leftNode;
			parent.right = rightNode;
			//4.从ArrayList中删除处理过的二叉树,加入新的parent
			nodes.remove(leftNode);
			nodes.remove(rightNode);
			nodes.add(parent);
		}
		//返回赫夫曼树的头
		return nodes.get(0);
		
		
	}
	
}

//创建节点类
//为了让Node对象支持排序，Collections集合排序，让Node实现Comparable接口
class Node implements Comparable<Node>{
	int value; //结点权值
	Node left; //指向左子节点
	Node right; //指向右子节点
	
	//写一个前序遍历用来测试
	public void preOrder() {
		System.out.println(this);
		if(this.left!=null) {
			this.left.preOrder();
		}
		if(this.right!=null) {
			this.right.preOrder();
		}
	}
	
	public Node(int value) {
		this.value = value;
	}
	@Override
	public String toString() {
		return "Node [value=" + value + "]";
	}
	@Override
	public int compareTo(Node arg0) {
		// TODO Auto-generated method stub
		return this.value-arg0.value; //从小到大排序
	}
}
```

