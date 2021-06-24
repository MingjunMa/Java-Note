## CH7 IO

### 1. File

File是对文件和路径名的抽象表示，其包含一个路径名，路径名可能不存在于存储介质上。在Java中File类存在以下几种构造方法：

```java
//直接使用路径构造file
File file = new File("C:\\test.txt");
//使用父路径+子文件名构造file
File file1 = new File("C:\\","test.txt");
//使用其他file路径+子文件名构造file
File file2 = new File(file1, "test.txt");
```

##### 1.1 File创建文件

使用File创建文件时，使用的方法为 **createNewFile()** 。若要创建的文件已经存在则返回false，若要创建的文件不存在且路径名正确则创建并返回true。在创建文件时，需要进行try...catch进行异常捕捉。

```java
File file = new File("C:\\demo.txt");
try {
    file.createNewFile();
} catch (IOException e) {
    e.printStackTrace();
}
```

##### 1.2 File创建目录及多级目录

mkdir()方法用来创建单级目录，mkdirs()用来根据路径创建多级目录。

```java
File file = new File("C:\\demo");
file.mkdir();
File file1 = new File("C:\\demo\\demo2");
file1.mkdirs();
```

File类下的0方法参考：https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/io/File.html

---

### 2. 字节流

Java中读写文件通常使用流机制，一个流只有一个方向（输入或输出）。按照读取的形式分为字节流与字符流，**字节流用于读取或写入txt文本对象**，不用于读取图片、视频等类型文件。

##### 2.1 字节流写数据

字节流写数据通常用OutputStream抽象类中的实现类的方法来实现。

```java
//向File写数据
FileOutputStream fileOutputStream = new FileOutputStream("C:\\test.txt");
try {
    //此处'90'为ASCII码，当查看时发现写入的为'Z'
    fileOutputStream.write(90);
} catch (IOException e) {
    e.printStackTrace();
} finally {
    //任何IO操作都需要进行关闭，释放系统资源
    fileOutputStream.close();
}
```

字节流写数据的两种方式

.write(int b): 每次写入一个字节：举例如2.1

.write(byte[] b, int off, int len): 从字节数组中写入指定偏移及长度的字节

```java
FileOutputStream fileOutputStream = new FileOutputStream("C:\\test.txt");
//写入的字节数组，使用getBytes()方法转换为字节数组
byte[] bytes = "abcde".getBytes();
try {
    fileOutputStream.write(bytes);
} catch (IOException e) {
    e.printStackTrace();
} finally {
    fileOutputStream.close();
}
```

**字节流的追加写入：**在FileOutputStream中，默认为从文件开头写入。若实现追加写入则需要在new时，在第二个参数传入true作为启动追加的参数。

```java
FileOutputStream fileOutputStream = new FileOutputStream("C:\\test.txt", true);
```

##### 2.2 字节流读数据

字节流读数据通常用InputStream抽象类中的实现类的方法来实现。同写数据原理相同，当读数据读到字节末尾后会**返回-1**。

```java
//单字节读取数据，因为字节以ASCII码存储，故使用int类型变量接收读入的ASCII码
int b;
FileInputStream fileInputStream = new FileInputStream("C:\\test.txt");
while ((b=fileInputStream.read())!=-1){
    System.out.print((char)b);
}
fileInputStream.close();
```

字节流读数据的两种方式

.read()单字节读取数据如2.4

.read(byte[] bytes)字节数组读取数据

```java
//字节数组读取数据
FileInputStream fileInputStream = new FileInputStream("C:\\test.txt");
byte[] bytes = new byte[1024];
fileInputStream.read(bytes);
//使用new String()进行字节到字符串的转换
System.out.println(new String(bytes));
```

##### 2.3 字节缓冲流

在以上提到的字节流IO操作中，每次IO一个字节都需要对系统的底层产生调用，这样的方式降低了代码的运行效率。因此在IO操作中，Java提供了带有缓冲区（Buffer）的字节IO流操作机制，其可以累计多个字节后一次性读写，这样可以提高程序的运行效率。

在Java中使用BufferedInputStream及BufferedOutputStream来调用IO缓冲区，其构造方法为：

```java
BufferedInputStream bufferedInputStream = new BufferedInputStream(InputStream in);
BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(OutputStream out);
```

---

### 3. 字符流

当我们需要从txt文件中读写中文或读写视频图片时，由于使用字节流会造成中文字节乱码或图片视频出错，因此需要使用字符流。字符流的读写抽象类为Reader, Writer。

##### 3.1 字符流读数据

同字节流类似，可以每次读取一个字符或读取一个数组的字符。

```java
//读取一个字符
InputStreamReader inputStreamReader = new InputStreamReader(new FileInputStream("C:\\test.txt"));
inputStreamReader.read();
inputStreamReader.close();
```

```java
//读取一个字符数组
InputStreamReader inputStreamReader = new InputStreamReader(new FileInputStream("C:\\test.txt"));
char[] chars = new char[1024];
inputStreamReader.read(chars);
System.out.println(new String(chars));
inputStreamReader.close();
```

##### 3.2 字符流写数据

.write(int c): 写一个字符

.write(char[] c, int off, int len): 写一个字符数组

.write(String str, int off, int len): 写一个字符串

在使用字符流写时，需要注意在字符流的底层封装形式依然为字节流，因此每次写入的字符实际上是储存在buffer中，因此在不做任何操作下文件中是不会显示写入内容的，因为待写入的内容在buffer。这是需要**使用flush()冲刷字符**到内容中，才可以在被写内容中显示。举例如下：

```java
//每次写入一个字符
OutputStreamWriter outputStreamWriter = new OutputStreamWriter(new FileOutputStream("C:\\test.txt"));
outputStreamWriter.write(90);
//将字符流冲出缓存区
outputStreamWriter.flush();
outputStreamWriter.close();

//每次写入一个字符数组
char[] chars = {80,81,82};
outputStreamWriter.write(chars);

//每次写入一个字符串
String s = "demo";
outputStreamWriter.write(s);
```

##### 3.3 字符缓冲流

在字符流中依然提供了buffer缓冲区以提高系统调用的效率，其实现为BufferedReader与BufferedWriter。

其构造方法为：

```java
BufferedReader bufferedReader = new BufferedReader(Reader);
BufferedWriter bufferedWriter = new BufferedWriter(Writer);
```