多态允许不同类的对象对同意消息进行响应

## 分类

+ 编译时多态
  + 一般通过方法重载实现
+ 运行时多态**（大多是运行时多态）**
  + 程序运行时动态决定调用哪个方法

## 必要条件

+ 满足继承关系

+ 父类引用指向子类对象



练习：PolyProj项目

+ 向上转型
+ 向下转型

## instanceof

判断左边的对象是否是右边的实例

可以判断左侧对象是否满足右侧的特征

```java
if(two instanceof Cat) {
			Cat temp = (Cat)two;
			temp.eat();
			temp.run();
			System.out.println("two可以转换为Cat类型");
		}
		if(two instanceof Dog) {
			Dog temp2 = (Dog)two;
			temp2.eat();
			temp2.sleep();
			temp2.getSex();
			System.out.println("two可以转换为Dog类型");
		}
		if(two instanceof Animal) {
			System.out.println("two可以转换为Animal类型");
		}
		if(two instanceof Object) {
			System.out.println("two可以转换为Object类型");
		}
```

返回boolean

可以先向上转型 再向下转型

## 抽象类

+ abstract 帮助我们不要写无意义的代码
  + 不能和static、final、private一起用
  + 因为final不能被重写
  + private 私有也不能被子类调用重写了
  + static也不能被子类重写了

+ 写在class前，类称为抽象类，**代表这个类不能被实例化**，可以和public位置互换
  + 实例化时可以指向子类实例 向上转型，然后再向下转型。

+ abstract写在方法前会变成抽象方法，可以用到父类的某些方法中，这个方法将变得不能有方法体（大括号不能有），不能直接被使用，且在子类的编写中，父类的抽象方法必须要进行重写，
  + 在这里如果不想在这个子类中重写这个方法，把这个子类变成抽象类也可以
+ 抽象方法必须在抽象类里，抽象类可以没有抽象方法

## 接口

如果希望一个类型中同时兼任不铜类型的特征

按照功能来定义 使用implements实现接口

在类中要有对接口中方法的重写

当接口指向实例化对象，接口能使用的方法只有自己本身有的，别的不能调用

### 接口的语法规则

+ 访问修饰符通常为public 和默认的访问权限
+ 接口中的抽象方法可以不加abstract关键字
+ 子类重写父类方法时 访问权限要大于等于父类，接口也这样
+ 当类实现接口时，必须实现接口中所有抽象方法（没大括号的都算），不然就得把类变成抽象类
+ 接口中可以包含常量，前面不用关键字修饰也是常量，默认public static final 可以通过接口名.来进行访问
+ 如果实现类中有和接口同名的常量，调用的都是接口里的内容
+ 接口里写的方法都是抽象方法
  + 除非
    + default默认方法，可以带方法体 也可以重写
    + static静态方法，可以带方法体 无法在实现类中重写重写
    + 上面的方法想访问就只能用`接口名.super.`
+ 一个类可以继承一个父类并实现若干接口
  + 接口多了，里面有相同方法的时候，使用这个方法就重写吧
  + 当父类和接口有一样的方法，调用也要用接口名或者super 不然不能自动识别

## 接口的继承

接口内部也可以继承接口，而且可以有多个爹

实现类中必须实现全部方法

如果多个父接口同时存在同名方法，作为子接口会不知道使用谁的，用default创建一个自己的同名的方法才行

## 内部类

将一个类定义在另一个类或一个方法里面

可以更好的封装

+ 成员内部类
  + 访问：
    + new一个外部类的对象，然后new 外部类.new 内部类
    + new一个外部类对象，外部类对象.new内部类
    + 在外部类对象中设置get获取方法
  + 访问修饰符可以任意，但范围受影响
  +  内部类中可以直接使用外部类的信息 ，也可以自己设置，优先访问自己的
  + 外部类访问内部类需要先实例
+ 静态内部类
  + static修饰
  + 调用外部类中的方法时，如果是静态方法可以直接调用，如果不是，需要创建一个实例 用对象去调。
  + 访问：
    + new一个外部类的对象，然后new 外部类.new 内部类
    + 可以通过外部类.内部类.静态成员的方式访问内部类中的静态成员
    + 如果要访问外部类静态属性，可以通过外部类.属性的方式
    + 如果要访问外部类非静态属性，需要通过实例化对象，对象访问
  + 里面也可以增加静态方法和静态属性
+ 方法内部类
  + 定义在方法里
  + 是局部的
  + 对方法成员的约束对它都有效
  + class前不可以添加public、private、protected、static
  + 类中不能包含静态成员
  + 类中可以有final、abstract修饰的成员
+ 匿名内部类
  
  + ```java
    public void getRead(Person person){ //参数传入父类对象
    	person.read();
    }
    public static void main(String[] args){
    	PersonTest test = new PersonTest(); 
    	test.getRead(new Person(){  //调用父类对象，直接在实例化过程中重写其中的read方法
    		@Override
            public void read(){
                System.out.println("男读书")
            }
    	})
    }
    ```
  
    更适用于程序中只用到这个类的一个实例时
  
    也无法使用public、private、protected、static、abstract等修饰
  
    无法编写构造方法，可以添加静态代码块，里面不能有静态成员
  
    匿名内部类可以继承父类，也可以实现接口，但是只能二选一

