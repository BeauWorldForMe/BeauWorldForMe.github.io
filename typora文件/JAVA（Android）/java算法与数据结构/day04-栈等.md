+ 出栈pop 入栈push
+ 

![image-20210622133634066](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210622133634066.png)

+ 数组模拟栈

  ```java
  package stackPorj;
  
  import java.util.Scanner;
  import java.util.Stack;
  
  public class ArrayStackDemo {
  
  	public static void main(String[] args) {
  		// TODO Auto-generated method stub
  		//测试一把
  		ArrayStack arrayStack = new ArrayStack(4);
  		String key = "";
  		boolean loop = true;//控制是否退出菜单
  		Scanner scanner = new Scanner(System.in);
  		while(loop) {
  			System.out.println("show:显示栈");
  			System.out.println("exit:退出程序");
  			System.out.println("push:添加数据到栈");
  			System.out.println("pop:从栈取出");
  			System.out.print("请输入：");
  			key = scanner.next();
  			switch(key) {
  			case "show":
  				arrayStack.list();
  				break;
  			case "push":
  				System.out.print("请输入数据：");
  				int data = scanner.nextInt();
  				arrayStack.push(data);
  				break;
  			case "exit":
  				loop=false;
  				break;
  			case "pop":
  				System.out.println(arrayStack.pop());
  				break;
  			default:
  				break;
  			}
  		}
  
  	}
  
  }
  
  class ArrayStack{
  	private int maxSize;//栈大小
  	private int[] stack;//数组模拟栈
  	private int top = -1;//栈顶
  	public ArrayStack(int maxSize) {
  		this.maxSize = maxSize;
  		stack = new int[this.maxSize];
  	}
  	//栈满
  	public boolean isFull() {
  		return top==maxSize-1;
  	}
  	//栈空
  	public boolean isEmpty() {
  		return top==-1;
  	}
  	//入栈-push
  	public void push(int value) {
  		//判断是否满
  		if(isFull()) {
  			System.out.println("栈满");
  			return;
  		}
  		top++;
  		stack[top] = value;
  	}
  	//出栈-pop
  	public int pop() {
  		//判断是否空
  		if(isEmpty()) {
  			throw new RuntimeException("栈空");
  		}
  		int value = stack[top];
  		top--;
  		return value;
  		
  	}
  	public void list() {
  		for(int i=top;i>=0;i--) {
  			System.out.printf("stack[%d]=%d\n",i,stack[i]);
  		}
  	}
  	
  }
  ```

  

![image-20210622161125797](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210622161125797.png)

