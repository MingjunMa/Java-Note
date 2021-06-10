## OOP (Object-Oriented Programming)

### 1.面向对象定义

以类的方式组织代码，以object形式进行数据、方法的封装。在面向对象的实现中依然是面向过程的。在Java中面向对象是将对象抽象化，其三大特性为**封装、继承、多态**。

---

### 2.类结构

一个类中存在属性和方法，其具体结果如下：

```java
public class Person{
    //属性
    String name;
    int age;
    
    //方法
    public void eat(){
        /*code...*/
    }
}
```

---

### 3.创建对象

使用**new关键字**来创建对象，会分配相应的内存空间，并进行默认初始化及无参构造，以上述Person类为例

```java
//new一个Person对象
Person person = new Person();
//获得对象属性
System.out.println(person.name);
//调用对象方法
person.eat();
```

---

### 4.构造器、有参构造、无参构造

***构造器**：是一种与**类名相同**，且**没有包含void在内的任何返回类型**的一种方法。其在类对象实例化时必须调用。

以3.创建对象中的person类举例，当程序执行 **Person person = new Person();** 时，实际是在调用class Person中的构造器 **public Person(){ }**。下图为编译后的Person.class文件中的构造器Person(){}。

<img src="assets/image-20210608232752741.png" alt="image-20210608232752741" style="zoom:50%;" />

**无参构造**：指的是在不引入参数的情况下，修改Person中的代码内容，实例化对象的初始值。举例如下：

```java
public class Person {
    String name;
    //无参构造
    public Person(){
        this.name = "ABC";
    }
}

```

```java
public class test{
    public static void main(String[] args) {
        Person person = new Person();
        System.out.println(person.name);
    }
}

output： ABC
程序打印结果为无参构造时预先设定的name参数"ABC"
```

***有参构造**：有参构造指的是，在Person.java文件中重载Person()并预先定义Person中的属性值。**若使用有参构造，则在Person.java中务必存在无参构造的显式形式**，举例如下：

```java
public class Person {
    String name;
    //若存在有参构造，则无参构造必须显式表示
    public Person(){}
    //有参构造，重写Person，将调用时传入的参数作为对象的name
    public Person(String name){
        this.name = name;
    }
}
```

在存在无参构造时，当调用Person时，若传入参数，则会在初始化person实例时使用Person(String name)方法来构造对象。如下：

```java
public class test{
    public static void main(String[] args) {
        //使用有参构造初始化person
        Person person = new Person("ABC");
        System.out.println(person.name);
    }
}

output： ABC
程序打印结果为初始化时输入的参数"ABC"
```

---

### 5.封装

指的是在设计一个类时，类的内部属性禁止从外部访问，通过方法接口来访问，实现高内聚，低耦合的设计。通过封装，可以提高程序的安全性，保护数据，隐藏代码的细节，提高可维护性。在封装中一般对属性进行get和set的操作。以Person类为例子：

```java
public class Person{
    //使用private对name和age进行封装
    private String name;
    private String age;
    //通过方法来对name进行操作
    //get操作
    public String getName(){
        return name;
    }
    //set操作
    public void setName(String name){
        this.name = name;
    }
}
```

---

### 6.继承

指的是对某一批类的抽象，在Java中类**只有单继承没有多继承**，用关键字**extends**来实现，通过继承，子类可以拥有父类全部的属性和方法。以Animal、Dog类为例：

```java
public class Animal{
	//父类的三种属性
    public String Name = "animal";
	protected int Age = 0;
	private char Sex = 'M';
	
    //父类的方法
    public void setName(String name){
        this.name = name;
    }
    public void eat(){
    	/*code...*/
	}
}

public class Dog extends Animal{
	public void bark(){
        System.out.println("wf!");
    }
}

public class Test {
    public static void main(String[] args) {
        Dog dog = new Dog();
        System.out.println(dog.Name);
        System.out.println(dog.Age);
        dog.setName("Siri");
        System.out.println(dog.Name);
        dog.bark();
    }
}

output:
    animal	//子类继承父类public属性，Name在子类未做更改，故输出"anamial"
    0	//子类继承父类protected属性

    Siri //子类更改继承的父类属性，将名字从"animal"改为"Siri"
    wf!	//子类使用自定义方法
```

两个类之间的继承关系示意图如下，可见**子类可以继承父类全部的public和protected属性和方法**，**不能继承private的属性和方法**。同时**子类可以添加独有的属性和方法**。

<img src="assets/image-20210609214725021.png" alt="image-20210609214725021" style="zoom:50%;" />

---

### 7. Super关键字

super是一种应用在**子类中的关键字**，其目的是**调用父类的public/protected属性、方法以及构造方法**。下面将通过Animal类和Dog类进行说明。

##### 7.1 调用父类属性、方法举例

```java
Animal父类
public class Animal{
    //父类的属性
    public String name = "animal";

    //父类的方法
    public void eat(){
        System.out.println("Animal: Eat food!");
    }
}

Dog子类
public class Dog extends Animal{
    public String name = "dog";

    public void eat(){
        System.out.println("Dog: Eat meat!");
        super.eat();
    }

    public void showName(){
        System.out.println("I'm " + name);
        System.out.println("I'm " + this.name);
        System.out.println("I'm " + super.name);
    }
}

Test测试类
public class Test {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();
        dog.showName();
    }
}

output:
Dog: Eat meat！
Animal: Eat food!
I'm dog
I'm dog
I'm animal
```

从测试结果可见，使用super关键字可以访问父类中public/protected的属性和方法，在子类中使用this.name和name都是访问该类中的属性。

##### 7.2 super与无参构造方法

在初始化子类时，调用构造方法时，即使未显示地显示super()关键字，代码也会自动执行父类的无参数构造后再执行子类的无参构造方法。

举例如下：

```java
public class Animal{
    //父类的无参构造方法
    public Animal(){
        System.out.println("animal: Parameterless construction");
    }
}

public class Dog extends Animal{
    //子类的无参构造方法
    public Dog() {
        System.out.println("dog: Parameterless construction");
    }
}

public class Test {
    public static void main(String[] args) {
        Dog dog = new Dog();
    }
}

output:
animal: Parameterless construction
dog: Parameterless construction
```

在输出中可见，先调用了父类的无参构造方法后调用了子类的无参构造方法，可见在子类无参构造代码中实质为：

```java
public class Dog extends Animal{
    //子类的无参构造方法
    public Dog() {
        //super默认为非显示形式
        super();
        System.out.println("dog: Parameterless construction");
    }
}
```

---

8. ### 重写(Override)
