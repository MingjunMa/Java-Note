### 1. 创建文件夹

```java
try {
  //在 $HOME 目录下创建文件夹
  new File(System.getProperty("user.home") + "/dir1/dir2").mkdirs();
}catch (IOException e){
  e.printStackTrace();
}
```



### 2. 写/读 文件

```java
try {
  BufferedWriter bw = new BufferedWriter(new FileWriter(file_path));
  bw.write("init");
	bw.close();
}catch (IOException e){
	e.printStackTrace();
}

try {
  BufferedReader br = new BufferedReader(new FileReader(file_path));
  //读一行，当此代码放入循环时，会读完一行后读下一行
  bw.readLine();
  //按要求读，看文档
  bw.read();
	bw.close();
}catch (IOException e){
	e.printStackTrace();
}
```

###### **使用 FileWriter(String path, boolean true); 方法写数据时，第二个参数默认为true，在写时会覆盖原来的文件，若不想覆盖则 第二个参数应为false**



### 3. 读/改/删 文件的某一行

```java
List<String> fileContent = new ArrayList<>(Files.readAllLines(Paths.get(data_path), StandardCharsets.UTF_8));

//read
fileContent.get(int index);
//edit
fileContent.set(int index, String newContent);
//remove
fileContent.remove(int index);

//重写更改后的文件
Files.write(Paths.get(data_path), fileContent, StandardCharsets.UTF_8);
```

###### **使用list容器将文件所有行读入到fileContent中，后通过.get(int index)方法获得行内容，file中第一行索引为0**