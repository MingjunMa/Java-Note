## Method

### 1.方法的定义
System(类).out(输出对象).println(方法)。方法包含于类或对象中。

Java中执行某一功能的一类代码称为方法，其实质等同于C语言中的函数。一般而言Java中的方法由方法头和方法体组成。方法头包括修饰符(public,private,static...)，返回类型(int,void...)，方法名称及传入参数组成。方法体中则为具体的实现代码。 **方法名+参数=方法签名**

根据Java规范，方法应该遵循**原子性**，即一个方法中仅完成一个功能，方法的名称应该遵循**驼峰命名法**。

![img](assets/D53C92B3-9643-4871-8A72-33D491299653.jpg)

---

### 2.形式参数与实际参数

形式参数指的是方法在定义时传入的参数，实际参数指的是方法在被调用时传入的参数。

```java
public static void main(String args[]){
    //实际参数1, 2
    add(1,2);
}

//形式参数num1, num2
public static void add(int num1, int num2){
    /*code...*/
}
```

---

### 3.方法的调用

返回值使用return，return在该方法最外层的括号里。如果值在if等语句里，则在语句里赋值比如result，然后最后最外层括号写return result；return也意味着终止方法了。

若一个方法有返回值，则方法的调用被当成一个值，采用赋值形式，如int max = max(a,b);

若一个方法无返回值，则方法调用一定是一个语句，采用obj.method(args[])形式调用，如System.out.println();

Java只有值传递，没有引用传递。
![image](https://user-images.githubusercontent.com/88830625/129857811-862674fc-20c8-43c5-85ee-0f213d8fa9d0.png)

---

### 4.方法的重载(Overload)

在一个类中，存在不同参数但方法名相同情况，这种情况称为重载。在重载中，两个方法的名字一定相同，参数列表(参数个数，参数类型，参数排列顺序等)一定不同，方法的返回类型可以相同也可以不同。

```java
public class test{
    public static void main(String args[]){
    	//根据传入参数不同，选择不同方法进行调用
        //调用add(int num1, int num2){}
        add(1,2);
        //调用add(char c){}
        add('a');
    }
    
    //不同参数列表重载
    public static void add(int num1, int num2){}
    public static void add(char c){}
    
    //不同返回类型重载，前提为参数列表不同
    public static void add(int num1, int num2){}
    public static int add(char c){}
}
```

---

### 5.方法中的可变参数

由于在应用中无法确定输入方法中参数的个数，因此采用可变参数来进行参数的传入。可变参数使用‘...’来表示，必须放到参数列表的最后一项，而且传入该参数位置的参数必须是同一类型的。

```java
public static void test(int num, double... num2){}
```

在调用时与普通方法调用相同。

```java
test(1, 1.1, 1.2, 1.3);
```

---

### 6.递归方法

递归指的是在某一方法内调用该方法，递归结构包含递归头和递归体，递归头决定何时停止对自身的调用，若无递归头则程序陷入死循环造成栈溢出。递归体决定何时调用自身方法。

以解决阶乘问题为例：

```java
public static int fac(int num){
    //递归头
    if (num == 1){
        return 1;
    }
    //递归体
    return num*fac(num-1);
}
```
---

### 7.静态方法与非静态方法

**静态方法**采用关键字static，静态方法与非静态方法区别在于，在不同类A,B中，若class A中存在**可访问的静态方法**，则在class B中无需new一个A对象即可以直接调用A中的静态方法。如：

```java
//静态方法举例
public class A{
	public static void test(){
        System.out.println("From A");
    }
}

public class B{
    public static void main(String[] args){
        //直接调用 类名.方法()
        A.test();
    }
}

output:"From A"
```

**非静态方法**中则不可直接调用，需要先new一个类对象后，通过对象中的方法调用。

```java
//非静态方法举例
public class A{
	public void test(){
        System.out.println("From A");
    }
}

public class B{
    public static void main(String[] args){
        //new实例对象后调用
        A a = new A();
        a.test();
    }
}

output:"From A"
```

**静态方法生命周期**：静态方法随着类的初始化而初始化，且仅初始化一次。因此若存在A,B两个方法，A为静态方法，若该方法中使用了非静态方法B，则编译会报错，这是因为在A静态方法随着类初始化时，无法获得未初始化的非静态方法B。需要实例化后才可调用。

```java
public class Demo{
	public static void A(){
		B();
	}
	
	public void A(){}
}

output: error
```
