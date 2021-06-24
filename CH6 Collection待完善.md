## CH6 Collection

### 1. Collection 定义

Collection指的是**集合**，也被翻译为**容器**。是Java中一类用来存放数据的结构。常见的collection和关系如下图所示。

<img src="assets/java-collection-hierarchy.png" alt="See the source image " style="zoom:50%;" />

---

### 2. 泛型

泛型是一个用来规范容器内存放数据类型的标识符，通常以'<E>'出现在容器类后，如：

```java
class Collection<E>{
    Object[] objects = new Object[10];
    public void set(E e, int index){
        objects[index] = e;
    }
    public E get(int index){
        return (E) objects[index];
    }
}
```

在实际调用中，对参数E进行类型赋值后即可以规定Collection中的类型。如：

```java
 public static void main(String[] args) {
    //对collection中的E进行String类型赋值后，容器collection中仅能存放字符串类型数据
    Collection<String> collection = new Collection<String>();
    collection.set("1a",0);
    String test = collection.get(0);
    System.out.println(test);
}
```

---

### 3. ArrayList

ArrayList是List的一个接口实现，是一个可以**动态变化**的数组。其为有序可以重复的容器，有序体现在容器内每一元素都有索引标识，重复体现在容器内允许存在equals()方法中返回相同的元素，底层实现为数组。

**特点**：查询效率高，增删效率低，线程不安全。

```java
//定义ArrayList, 其中E为泛型，需要赋以类型
ArrayList<E> arrayList = new ArrayList<E>();
```

具体方法详解见：https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/ArrayList.html

ArrayList 底层使用可扩容数组，扩容后容量=Last容量+(Last容量>>1)。扩容后将原数组拷贝到新数组，从而完成数组的扩容。扩容底层代码如下(java版本为：java 11.0.10 2021-01-19 LTS)：

```java
private int newCapacity(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity <= 0) {
            if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA)
                return Math.max(DEFAULT_CAPACITY, minCapacity);
            if (minCapacity < 0) // overflow
                throw new OutOfMemoryError();
            return minCapacity;
        }
        return (newCapacity - MAX_ARRAY_SIZE <= 0)
            ? newCapacity
            : hugeCapacity(minCapacity);
    }
```

---

### 4. LinkedList

LinkedList为List接口、Queue接口、Deque接口的实现，是一个非连续存储的数据结构。每一节点包含3部分：前驱(pre)、数据(data)、后继(next)。

**特点**：查询效率低，增删效率高，线程不安全。

```java
LinkedList<String> linkedList = new LinkedList<String>();
```

Java中提供的LinkedList的方法见：https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/LinkedList.html

---

### 5. HashMap

HashMap是Map接口的一个接口实现，是一种以**键值对**形式存储数据的数据结构，**每个键要唯一**，若键重复则覆盖之前的键。

<img src="assets/java-map-hierarchy.png" alt="Java Map Hierarchy " style="zoom:50%;" />

Java中使用HashMap如下：

```Java
//<Key, Value>为泛型，规定键值对的数据类型
HashMap<Key, Value> hashMap = new HashMap<Key, Value>();
//添加数据
hashMap.put(key, data);
//根据键值移除数据
hashMap.remove(key);
```

Java中HashMap提供方法：https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Map.html

**HashMap底层原理**：底层使用哈希表，这是一种结合数组和链表优点的数据结构。使用数组来作为连续的索引，计算将要存入数据的哈希值，使用不同的散列法得到对应的索引位置，如遇到哈希冲突(索引位置已存在数据)，则使用链表将数据连接到该位置上一数据的next指针处。示意图如下：

<img src="assets/R8c0ce6de1fb2f81d18dd2c13b8701026" alt="See the source image " style="zoom:50%;" />

在Java中，HashMap使用的散列方法为改进的相除取余法，其约定作为索引的数组长度为2的整数幂，使用 **hash值 = hashcode&(len-1)** 来计算散列后的存储位置。在JDK8以后，当链表大于8后使用红黑树而非链表。

常用散列方法：https://www.cnblogs.com/huangfox/archive/2012/07/06/2578898.html

---

### 6. Set及Treeset

---

### 7. Iterator

为一种迭代器，用来遍历容器。

```java

```

---

### 8. Collection类

对容器内的元素进行排序
