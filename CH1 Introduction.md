## Introduction

### 1. JDK, JRE, JVM

JDK(Java Development Kit): 是Java开发中使用的工具，提供开发、编译等功能。

JRE(Java Runtime Environment): Java运行环境，是Java程序在运行时所依赖的环境文件，仅安装JRE无法进行Java的开发，但是可以运行Java程序和应用。

JVM(Java Virtual Machine): Java虚拟机运行环境，是Java跨平台运行的核心，提供Java程序与系统底层之间的交互。

<img src="assets/R4f1ba2599978af4366d80742cf9c579e" style="zoom:70%;" align='left'/>



### 2.数据类型

Java为强类型语言，要求变量先定义后使用。Java数据类型分为基本类型和引用类型。

**基本类型**

| 名称    | 大小  | 范围                                |
| ------- | ----- | ----------------------------------- |
| byte    | 1字节 | -128-127                            |
| short   | 2字节 | -32768-32767                        |
| int     | 4字节 | -2147483648-2147483647              |
| long    | 8字节 | 在定义式后加L, long a = 10L;        |
| float   | 4字节 | 在定义式后加F, float a = 1.1F;      |
| double  | 8字节 |                                     |
| char    | 2字节 | 单引号内仅有一个字符, char c = 'A'; |
| boolean | 1位   | true，false                         |

注：在进行较为精确的小数运算时，禁止使用float与double，会造成运算的精度错误，应改用Java的大数运算类。

类型转换(低->高)：byte -> short -> char -> int -> long -> float -> double

类型转换(高->低)：type_des value = (type_des)value_ori;

类型高转低会遇到诸如内存溢出，数值精度错误等。

**引用类型**

包含类(class), 接口(interface), 数组等。



### 3.包机制

Java包等价于文件夹，包名一般使用公司域名导致作为包名。在引用时使用import package.name.* 。