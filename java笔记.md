# java

## 概要

### 基础常识

1. 软件开发

   1. 系统软件
   2. 应用软件

2. 人机交互方式

   1. 图形化界面

   2. 命令行方式

      1. 常用的DOS命令

         ```shell
         1. dir	#列出当前目录下的文件以及文件夹
         2. md	#创建目录
         3. rd	#删除目录
         4. cd	#进入指定目录
         5. cd ..
         6. cd \
         7. del	#删除文件
         8. exit	#退出dos命令行
         ```



### java语言概述

 1. 什么是计算机语言

    人与计算机交流的方式

	2. 语言历史

    	1. 第一代语言
        	1. 打孔机--纯机器语言
    	2. 第二代语言
        	1. 汇编
    	3. 第三代语言
        	1. C、Pascal、Fortran面向过程的语言
        	2. C++面向过程/面向对象
        	3. java跨平台的纯面向对象的语言
        	4. .NET跨语言的平台

    面向过程，例如张三打篮球，还要在做一个李四踢足球的程序？

    面向对象，例如  人的对象，人运动的动作，人运动的器械

    ​	实例化一个张三的对象，这个对象有一个打篮球的动作，器械是篮球

    ​	实例化一个李四的对象，这个对象有一个踢足球的动作，器械是足球

    面向对象能够更好的再抽象的层面来分析问题，在程序实现跨越极大的赋予之前的代码

    这些是面向过程变成很难实现的。

    

### java程序运行机制

 1. java语言的特点

     	1.	面向对象
          	1.	两个基本概念：类，对象
          	2.	三大特性：封装、继承、多态

 2. 健壮性  完善性

 3. 跨平台性   jvm

    原理：只要在需要运行java应用程序的操作系统上，先安装一个java虚拟机（JVM java Virtual Machine）即可。由JVM来负责java程序在该系统的运行



​	核心机制-垃圾回收

**c  c++**

​	由程序员手动编写代码回收（优点：能够再内存不使用时快速回收，准确高效；缺点：容易出bug   内存溢出）

​	

**java**

​	自动回收，开了一个系统集线程自动去检测哪些内存不用了然后回收掉

​	缺点：回收不及时；

### java语言环境的搭建

 1. 下载JDK

 2. 安装JDK

 3. 配置环境变量

    JAVA_HOME

    ```SHELL
    #JDK路径
    C:\Program Files\Java\jdk-11.0.2
    ```

    CLASSPATH

    ```SHELL
    .;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;
    ```

    PATH

    ```SHELL
    %JAVA_HOME%\bin
    %JAVA_HOME%\jre\bin
    ```

    

 4. 验证是否成功：

    ```shell
    java --version
    ```



JDK(java Development Kit)  java开发工具包

​	包含了java的开发工具（javac.exe），JRE

JRE ()	java运行环境



jvm 《  jre 《 jdk



### 开发体验-helloworld

```java
public class Text{
	public static void main(String[] args){
		System.out.print("hello world");
	}
}
```



### 小结 第一个程序

1. java源文件以“java”为扩展名。源文件的基本组成部分是类（class）

2. java应用程序的执行入口是main()方法。他有固定的书写格式。

   ```java
   public static void main(String[] args){...}
   ```

3. java语言严格区分大小写

4. java方法由一条条语句构成，每个语句以“;”结束

5. 括号都是成对出现，缺一不可

### 常见问题及解决方法

​	文件名和内容里的class  名 要一致

![image-20201119101217676](C:\Users\zdwljs\AppData\Roaming\Typora\typora-user-images\image-20201119101217676.png)

​	

java  后面不要.

![image-20201119101256200](C:\Users\zdwljs\AppData\Roaming\Typora\typora-user-images\image-20201119101256200.png)



一定要注意分号;

### 注释

```java
//单行注释
//

//多行注释
/* 
xxx
xxx
*/

//文档注释(java特有)

/**
*文档注释
*这是一个打印hello world的类
*@author liuzheng
*@version 1.0.0
*/
```



## Java基本语法1

### 关键字

 1. 关键字的定义和特点

    定义：被java语言赋予了特殊含义，用做专门用途的字符串（单词）

    特点：关键字中所有字母都为小写

    

    用于定义数据类型的关键字

    | calss   | interface        | enum  | byte   | short |
    | ------- | ---------------- | ----- | ------ | ----- |
    | int     | long             | float | double | char  |
    | boolean | void(没有返回值) |       |        |       |

    用于定义数据类型值的关键字

    | true | false | null |
    | ---- | ----- | ---- |
    |      |       |      |

    用于定义流程控制的关键字

    | if     | else | switch | case  | default  |
    | ------ | ---- | ------ | ----- | -------- |
    | while  | do   | for    | break | continue |
    | return |      |        |       |          |

    用于定义访问权限修饰符的关键字

    | Private | Protected | Public |
    | ------- | --------- | ------ |
    |         |           |        |

    用于定义类，函数，变量修饰符的关键字

    | abstract | final | static | synchronized |
    | -------- | ----- | ------ | ------------ |
    |          |       |        |              |

    用于定义类与类之间关系的关键字

    | extends | implements |
    | ------- | ---------- |
    |         |            |

    用于定义建立实例及引用实例，判断实例的关键字

    | new  | this | super | instanceof |
    | ---- | ---- | ----- | ---------- |
    |      |      |       |            |

    用于异常处理的关键字

    | try  | catch | finally | throw | throws |
    | ---- | ----- | ------- | ----- | ------ |
    |      |       |         |       |        |

    用于包的关键字

    | package | import |
    | ------- | ------ |
    |         |        |

    其他修饰符的关键字

    | native | strictfp | transient | volatile | assert |
    | ------ | -------- | --------- | -------- | ------ |
    |        |          |           |          |        |

    保留字：

    byValue、cast、futrue、generic、inner、operator、outer、rest、var、goto、const

### 标识符

​	规则：

		1.	由26个英文字母大小写，0-9，_或者$组成
  		2.	数字不可以开头
    		3.	不可以使用关键字和保留字，但能包含关键字和保留字
      		4.	java中严格区分大小写，长度无限制
        		5.	标识符不能包含空格



​	名称命名规范：

 1. 包名：

    多单词组成时所有字母小写：xxxyyyzzz

	2.	类名、接口名：多单词组成时，所有单词首字母大写：XxxYyyZzz

	3.	变量名：方法名：多单词组成时，第一个单词首字母小写，第二个单词开始每个首字母大写：xxxYyyZzz

	4.	常量名：所有字母大写，多单词用下划线链接：XXX_YYY_ZZZ

### 变量

概念：

			1.	内存中的一个存储区域
   			2.	该区域有自己的名称（变量名）和类型（数据类型）
      			3.	java中每个变量必须先声明，后使用
         			4.	该区域的数据可以再同一类型范围内不断变化

使用变量注意：

			1.	变量的作用域：一对{}之间有效
	
			2.	初始化值：第一次给变量赋值
	
	  int m;  这是不对的
	
	  int i = 1;

定义变量的格式

​		数据类型	变量名 = 初始化值

变量是通过使用变量名来访问这块区域的



变量的分类-按数据类型

​	对于每一种数据都定义了明确的具体数据类型，在内存中分配了不同大小的内存空间。

​	基本数据类型

​			数值型	

​				整数类型	   byte  short  int   long

​				浮点类型	   float	double

​			字符型	char

​			布尔型	boolean

​	引用数据类型

​			类	calss	(String)

​			接口	interface

​			数组	[]

#### 一、基本数据类型

##### 1. 整数类型	byte  short  int   long

​	整数类型常量默认为int，声明long类型需后面加 “l”或“L”

| 类型  | 占用存储空间 | 表数范围     |
| ----- | ------------ | ------------ |
| byte  | 1字节 = 8bit | -128~127     |
| short | 2字节        | -2^15~2^15-1 |
| int   | 4字节        | -2^31~2^31-1 |
| long  | 8字节        | -2^63~2^63-1 |

##### 2.浮点类型 	float	double

​	浮点类型 常量默认为double，声明float类型需后面加 “f”或“F”

| 类型         | 占用存储空间 | 表数范围       | 精度         |
| ------------ | ------------ | -------------- | ------------ |
| 单精度float  | 4字节        | -2^128~2……128  | 7位有效数字  |
| 双精度double | 8字节        | -2^1024~2^1024 | 16位有效数字 |

##### 3.字符类型 char

​		char型整数用来表示通常意义上的“字符” 2字节

​		表现形式：

​			字符常量是用单引号 '' 括起来的单个字符，涵盖世界上所有书面语的字符

​		char c1 = 'a';

​		char c2 = '中';

​		char c3 = '9';

​		char类型是可以进行运算的，因为它都对应有Unicode码



##### 4.布尔类型	boolean

​			boolean类型适用逻辑运算  一般用于程序流程控制

​			只允许取值true  false   无null

​			不可以0或非0的整数替代false或true

##### 5.引用类型  String类

​	值null可以赋值给任何引用类型（类、接口、数组）的变量，用以表示这个引用类型变量中保存的地址为空；

​	String类属于引用类型，可用null赋值；

​	String类型是一个典型的不可变类，String对象创建出来就不可能被改变。创建出的字符串将存放再数据区，保证每个字符串 常量只有一个，不会产生多个副本；



#### 二、基本数据类型转换

1. 自动类型转换

   容量小的类型自动转换为容量大的数据类型。

   ​	char

   byte				<	int	   <		long	  <		float		<	double

   ​		short

2. 有多种类型的数据混合运算时，系统首先自动将所有数据转换成容量最大的那种数据类型，然后再进行计算

3. byte,short,char之间不会相互转换，他们三者再计算时首先转换为int类型

4. 当把任何基本类型的值和字符串值进行连接运算时（+），基本类型的值将自动转化为字符串类型；

#### 三、基本数据类型转换

1. 自动类型转换的逆过程，将容量大的数据类型转换为容量小的数据类型。使用时要加上强制转换符（()），但可能造成精度降低或溢出，格外要注意；

   ```java
   int k = 7;
   byte b = (byte)k;
   ```

   

2. 通常，字符串不能直接转换为基本类型，但通过基本类型对应的包装类则可以实现把字符串转换成基本类型；

   ```java
   String a = "43";
   int i = Integer.parseInt(a);
   
   //boolean类型不可以转换为其他的数据类型
   ```

   

### 运算符

运算符是一种特殊的符合，用以表示数据的运算、赋值和比较等

1. 算术运算符

   1. +

      + 正号
      + 加法
      + 字符串连接

   2. -

      - 负号
      - 减法

   3. *

   4. /

      - 6 / 2 = 3
      - 7 / 2 = 3
      - 7.0 / 2 = 3.5

   5. %     取模   （取余数）   7%5  = 2 

      **如果对负数取模，可以把模数负号忽略不计   5%-2 = 1；

      **被模数是负数则不可忽略。  -5%2 = -1；

      **取模运算结果不一定总是整数

   6. ++   自增

      - 前  （赋值时  先运算后取值）

        a=2;

        b = ++a;

        =>  a=3;b=3

      - 后 （赋值时  先取值后运算）

        a=2;

        b=a++;

        a=3;

        b=2;

   7. --   同上

2. 赋值运算符   =

   当**“=”**两侧数据类型不一致时，可以使用自动类型转换或使用强制类型转换原则进行处理

   支持连续赋值

   扩展赋值运算符：

   ​	+=

   ​	-=

   ​	*=

   ​	/=

   ​	%=

   // 变量参与运算的时候，java程序不知道具体的这个变量再做完运算后会不会超出当前变量的范围，所以会先把变量转化为一个更大的长度（一般都是int类型）

   ```java
   short s = 2;
   s = s + 2; //编辑器报错   = 号左边的s 已经被转化为int了  所以不能赋值到short变量中。
   
   s = (short)(s + 2);
   //或者 +=
   s += 3;  //在使用扩展赋值运算符的时候，变量在参与运算时会把结果强制转换为当前变量的类型；
   ```

   

3. 比较运算符   关系运算符

   | 运算符 | 运算     | 范例    | 结果  |
   | ------ | -------- | ------- | ----- |
   | ==     | 相等于   | 4 ==3   | false |
   | ！=    | 不等于   | 4 ！= 3 | true  |
   | <      | 小于     | 4<3     | false |
   | >      | 大于     | 4>3     | true  |
   | <=     | 小于等于 | 4<=3    | false |
   | >=     | 大于等于 | 4>=3    | true  |

4. 逻辑运算符

   & 逻辑与(并且)	| 逻辑或(有一个条件成立就成立) 	！逻辑非

   && 短路与 || 短路或	^逻辑异或(a和b 其中一个成立  一个不成立)

   | a     | b     | a&b   | a\|b  | !a    | a^b   | a&&b  | a\|\|b |
   | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ------ |
   | true  | true  | true  | true  | false | false | true  | true   |
   | true  | false | false | true  | false | true  | false | true   |
   | false | true  | false | true  | true  | true  | false | true   |
   | false | false | false | false | true  | false | false | false  |

   在java中  3<x<6 是错误的

   x>3&x<6  

   

   & 和 && 的区别

   	1. & 时，左边无论真假，右边都进行运算；
    	2. &&，如果左边为真，右边参与运算；如果左边为假，那么右边不参与运算；

   

5. 位运运算符

   二进制运算

   | 运算符 | 运算       | 范例                                        |
   | ------ | ---------- | ------------------------------------------- |
   | <<     | 左移       | 3<<2 = 12 -> 3 * 2 * 2 = 12;  m<<n -> m*2^n |
   | >>     | 右移       | 3>>1 = 1   -> 3/2 = 1     m>>n -> m*2^-n    |
   | >>>    | 无符号右移 | 3>>>1 =1  ->  3/2=1                         |
   | &      | 与         | 6&3  2                                      |
   | \|     | 或         | 6\|3  7                                     |
   | ^      | 异或       | 6^3  5                                      |
   | ~      | 反码       | ~6  -7                                      |

   

6. 三元运算符

### 程序流程控制

​	for循环语句

```java
for(int i = 0;i<=100;i++){
    System.out.printLn(i);
}
```

​	while循环语句

```java
while(布尔值){
    
}
```

特殊流程控制语句

break 语句   用来终结某个语句块的执行

​	只用于switch 和 循环语句

continue 语句	用于跳过某个循环语句块的一次执行 

​	只能用于循环语句

return      结束一个方法



### 数组

```java
int i = 0;
int k = 1;
int m = 2;
int[] ii; //声明一个int的数组
```



 1. 一维数组

    type(数据类型)  var(变量名)[]

    type(数据类型)[] var(变量名);

    ```java
    int i[];
    int[] i;
    double b[];
    Mydate[] c;//对象数组
    
    int i[] = new int[4]  //声明一个能放4个int类型数据的数组
    ```

    一维数组初始化

    ```java
    //动态初始化
    int[] arr = new int[3];
    arr[0] = 1;
    arr[1] = 2;
    arr[3] = 4;
    //静态初始化
    int a[] = new int[]{3,9,8};
    int[] a = {3,9,8}
    ```

    数组元素的引用

    1. 定义并用运算符new为之分配空间后，才可以引用数组中的每个元素；
    2. 数组元素的引用方式：数组名[数组元素下标]
       1. 数组元素下标可以是整型常量或整型表达式  a[3]  b[i]  c[6*i]
       2. 数组元素下标从0开始；长度为n的数组合法下标取值范围0->n-1
    3. 每个数组都有一个属性length指明他的长度；
       1. **数组一旦初始化，其长度是不可变的**

    数组元素的默认初始化

    ​	数组时引用类型，他的元素相当于类的成员变量，因此数组一经分配空间，其中的每个元素也被按照成员变量同样的方式被隐式初始化

    数字类型  默认 0

    对象类型 默认 null

    ```java
    public class Test{
        public static void main(String args[]){
            int a[] = new int[5];
            System.out.printLn(a[3]) //0
        }
    }
    ```

 2. 多维数组

```java
int[][] arr = new int[3][2]
    //定义了名称为arr的二维数组
    //二维数组中有3个一维数组   每个一维数组中有2个元素
    //一维数组的名称分别为arr[0] arr[1] arr[2]
int[][] arr = new int[3][];
	//二维数组中有3个一维数组
	//每个一维数组都是默认初始化值null（区别于格式1）
	//可以对这个三个一维数组分别进行初始化
	arr[0] = new int[3];
	arr[1] = new int[1];
	arr[2] = new int[2];


//	int[][] arr = new int[3][2]
	int[][] arr = new int[][]{
        {1,2},
        {4,2},
        {4,2}
    }


	int[] x,y[];  //x是一维数组   y是二维数组
```

## 面向对象编程

### 面向对象与面向过程

	- 面向对象（OOP）与面向过程（POP）
 - 面向对象的三大特征
   	- 封装
      	- 继承
   	- 多态

### java语言的基本元素：类和对象

```java
class Person{
    String name;
    int age;
    boolean isMarried;
    
    public void walk(){
        
    }
    
    public String dispaly(){
        return ""
    }
}


修饰符 class 类名{
    	属性声明；
        方法声明；
}

修饰符 public  类可以被任意访问
    类的正文要用{}括起来
    

```

操作对象的变量

调用类方法

### 类的成员之一：属性

修饰符  类型  属性名 = 初值

​	修饰符 private   ： 该属性只能由该类的方法访问；**私有属性**

​	修饰符 public 	：该属性可以被该类以外的方法访问。 **公有属性**

​	类型：任何基本类型



变量的分类：成员变量、局部变量

在方法体外，类体内声明的变量称为成员变量；

在方法体内部声明的变量称为局部变量；

​					成员变量		 实例变量（不以static修饰）

​											 类变量（以staitc修饰）

所有变量								



​					局部变量			形参（方法签名中定义的变量）

​												方法局部变量（在方法内定义）

​												代码块局部变量（在代码块内定义）

 

### 类型的成员之二：方法

 修饰符	返回值类型	方法名（参数列表）{

}

修饰符： public 	private	protected

返回值类型:	return 传递返回值	  没有返回值：void

 

### 对象的创建和使用

  ```java
new 关键类 
  ```

每个对象都是独立，互不干扰


| 成员变量类型 | 初始值         |
| ------------ | -------------- |
| byte         | 0              |
| short        | 0              |
| int          | 0              |
| long         | 0L             |
| float        | 0F             |
| double       | 0.0D           |
| char         | '\u0000'（空） |
| boolean      | false          |
| 引用类型     | null           |



匿名对象

​	new Person().shout();

使用情况

​	如果对一个对象只需要进行一次方法调用，那么就可以使用匿名对象；

​	我们经常讲匿名对象作为实参传递给一个方法调用；



提示：

​	在一个类中的访问机制：类中的方法可以直接访问类中的成员变量（例外：static方法访问非static，编译不通过）

​	在不同类中的访问机制：先创建要访问类的对象。再用对象访问类中定义的成员



#### 面向对象思想“落地”法则（一）

1. 关注于类的设计，即设计类的成员：属性、方法
2. 类的实例化，即创建类的对象（new Person（））
3. 通过“对象.属性”  “对象.方法”  执行



### 再谈方法

	#### 方法的重载（overload）

​	在一个类中，允许存在一个以上的同名方法，只要他们的参数个数或者参数类型不同即可。



特点：

与返回值类型无关，只看参数列表，且参数列表必须不同（参数个数或参数类型）。调用时，根据方法参数列表的不同来区别



```java
int add(int x, int y){
    return x+y
}
int add(int x, int y, int z){
    return x+y+z
}
int add(double x,double y){
    return x + y
}
```

#### 体会可变个数的形参

```java
//没有参数就要定义一个空数组或者null
public void printInfo(int a,String[] books){
   	
    System.out.printLn();
}

//没有参数可以不填
// ... 代表可以传0-N个参数
public void printInfo(int a,String... books){
   	
    System.out.printLn();
}
```

说明：

	1. 可变参数：方法参数部分指定类型的参数个数是可变多个
 	2. 声明方式：方法名（参数的类型名...参数名）
 	3. 可变参数方法的使用与方法参数部分使用数组时一致的
 	4. 方法的参数部分有可变参数，需要放在形参声明的最后



**java里的方法的参数传递方式只有一种：值传递。  即将实际参数值的副本（复制品）传入方法内，而参数本身不受影响**



参数传递之引用对象

​	

#### 软件包

	1. 包帮助管理大型软件系统：将语义近似的类组织到包中；解决类名冲突的问题；
 	2. 包可以包含类和子包；

##### 关键字-package（包）

package语句作为java源文件的第一条语句，指明该文件中定义的类所在的包（若缺失，则指定为无名包）

```java
package 顶层包名.子包名
```



##### import （引用）

指明类在哪

JDK中主要的包介绍

1. java.lang-包含一些java语言的核心类，如String、Math、Interger、System、Thread，提供常用功能
2. java.net-包含执行与网络相关的操作的类和接口
3. java.io-包含能够提供多种输入/输出功能的类
4. java.util-包含了一些实用工具类，如定义系统特性、接口的集合框架类、使用与日期日历相关的函数
5. java.text-包含了一些java格式化相关的类
6. java.sql-包含了java进行JDBC数据库编程的相关类/接口
7. java.awt-包含了构成抽象窗口工具集（abstract  window  toolkits）的多个类，这些类被用来构建和管理应用程序的图形用户界面（GUI）
8. java.applet-包含applet运行所需的一些类

### 面向对象特征之一：封装和隐藏

信息隐藏

防止乱用

```java
package day01;

public class Person {
    private int age;  //私有属性
    public void showAge(){
        System.out.println(age);
    }

    public void setAge(int a){	 //封装
        if(a <= 150 && a>=0){
            age = a;
        }else{
            System.out.println("输入的年龄："+a+" 不在0-150之间");
        }
    }
}
```

#### 四种访问权限修饰符

public	protected	private 置于类的成员定义前，用来限定对象对该类成员的访问权限

| 修饰符    | 类内部 | 同一个包 | 字类 | 任何地方 |
| --------- | ------ | -------- | ---- | -------- |
| private   | yes    |          |      |          |
| （缺省）  | yes    | yes      |      |          |
| protected | yes    | yes      | yes  |          |
| public    | yes    | yes      | yes  | yes      |

对于class的权限修饰只可以用public   default（缺省）

public类可以再任意地方被访问

defalut类只可以被同一个包内部的类访问

### 类的成员之三  构造器（构造方法）

new对象实际就是调用构造方法

构造器特征

	1.	具有与类相同的名称
 	2.	不声明返回值类型
 	3.	不能被static、final、synchronized、abstract、native修饰，不能有returen语句返回值

注意：

	1. java语言中，每个类都至少有一个构造器
 	2. 默认构造器的修饰符与所属类的修饰符一致
 	3. 一旦显示定义了构造器，则系统不再提供默认构造器
 	4. 一个类可以创建多个重载的构造器
 	5. 父类的构造器不可被子类继承



**构造器的重载**

构造器一般用来创建对象的同时初始化对象。

构造器重载使得对象的创建更加灵活，方便创建各种不同的对象。

构造器重载，参数列表必须不同

### 几个关键字：super  this  package  import

 #### 关键字this

在java中，this关键字比较难理解，他的作用和其词义很接近。

​	它在方法内部使用，即这个方法所属对象的引用。

​	它在构造器内部使用，表示该构造器正在初始化的对象。

this表示当前对象，可以调用类的属性、方法和构造器

什么时候使用this关键字呢？

​	当在方法内需要用到调用该方法的对象时，就用this。

```java
//this() 
// 必须放到构造器的首行！！！
// 使用this调用本类中其他的构造器，保证至少有一个构造器是不用this的。
// 本质是 构造器自己不能调用自己
public class Person{
    public Person(){
        
    }
    public Person(int age){
        this.age = age;
    }
    public Person(int age,String name){ 
        this(age);//等同于调用构造方法 public Person(int age){
        this.name = name;
    }
    int age ;
    String name;
}
```



#### JavaBean

 JavaBean是一种java语言写成的可重用组件

所谓javaBean，是指符合如下标准的java类。

1. 类是公共的
2. 有一个无参的公共的构造器
3. 有属性，一般私有，且有对应的get、set方法

```java
/*
	一个JavaBean
	私有属性
	属性对应的get set方法
*/
public class Person{
    private String name;
    
    public void setName(String name){
        this.name = name;
    }
    public String getName(){
        return this.name;
    }
}

public class Person{
    private String name;
  
    //鼠标右键   Source-》  Generate Getters and Setters
    //自动生成
}
```



## 高级类的特性

### 面向对象特征之二：继承

 ```java
public class Student extends Person{
    
}
 ```

作用：

	1. 继承的出现提高了代码的复用性
 	2. 继承的出现让类与类之间产生了关系。提供了多态的前提。
 	3. 不要仅为了获取其他类中的某个功能而去继承



#### 类的继承

1. 子类继承了父类，就继承了父类的方法和属性
2. 在子类中，可以使用父类中定义的方法和属性，也可以创建新的数据和方法
3. 在java中，继承的关键字用的是  ```extend```，即子类不是父类的子集，而是对父类的“扩展”

关于继承的规则：

​	子类不能直接访问父类中私有的成员变量和方法。（通过setter或者getter）

#### java只支持单继承，不允许多继承

1. 一个子类只能有一个父类
2. 一个父类可以派生出多个子类
3. 可以多层继承

**多层继承**

​	父类1 -》  父类2 -》子类



### 方法的重写（override）

定义：	在子类中可以根据需要对从父类中继承来的方法进行改造，也称方法的重置，覆盖。在程序执行时，子类的方法将覆盖父类的方法。

要求： 

 1. 重写方法必须和被重写方法具有相同的方法名称、参数列表和返回值类型

    （子类重写父类的方法，只是重写编写方法体的代码）

 2. 重写方法不能使用比被重写方法更严格的访问权限。

 3. 重写和被重写的方法须同时为static的，或同时为非static的

 4. 子类方法抛出的异常不能大于父类被重写方法的异常

### 四种访问权限修饰符

| 修饰符    | 类内部 | 同一个包 | 字类 | 任何地方 |
| --------- | ------ | -------- | ---- | -------- |
| private   | yes    |          |      |          |
| （缺省）  | yes    | yes      |      |          |
| protected | yes    | yes      | yes  |          |
| public    | yes    | yes      | yes  | yes      |

如果子类和父类再同一个包下，那么对于父类的成员修饰符只要不是私有的private，那就都可以使用

如果子类和父类不在同一个包下，那么子类只能使用父类中protected和public修饰的成员和方法。

### 关键字super

在java类中使用super来调用父类中的指定操作

1. super可用于访问父类中定义的属性
2. super可以用于调用父类中定义的成员方法
3. super可以用于子类构造方法中调用父类的构造器

注意：

1. 尤其当子父类出现同名成员时，可以用super进行区分
2. super的追溯不仅限于直接父类
3. super和this的用法想像，this代表本类对象的引用，super代表父类的内存空间的标识



调用父类的构造器

	1. 子类中所有的构造器默认都会访问父类中**空参数**的构造器
 	2. 当父类中没有**空参数**的构造器时，子类的构造器必须通过this（参数列表）或者super（参数列表）语句指定调用本类或者父类中相应的构造器，且必须放在构造器的第一行
 	3. 如果子类构造器中既未显示调用父类或本类的构造，且父类中有没有无参的构造器，则编译出错。

注意：

​	在父类只有有参构造可以使用的时候，子类必须显示的构建一个构造来调用父类的有参构造，并且调用父类构造方法要写再第一行



this和super的区别

| no.  | 区别点     | this                                                   | super                                    |
| ---- | ---------- | ------------------------------------------------------ | ---------------------------------------- |
| 1    | 访问属性   | 访问本类中的属性，如果本类没有此属性则从父类中继续查找 | 访问父类中的属性                         |
| 2    | 调用方法   | 访问本类中的方法                                       | 直接访问父（级）类（多层父类）中的方法   |
| 3    | 调用构造器 | 调用本类构造器，必须放在构造器的首行                   | 调用父类构造器，必须放在子类构造器的首行 |
| 4    | 特殊       | 表示当前对象                                           | 无此概念                                 |





### 子类对象实例化过程

![image-20201214153951882](C:\Users\zdwljs\AppData\Roaming\Typora\typora-user-images\image-20201214153951882.png)

![image-20201214154255754](C:\Users\zdwljs\AppData\Roaming\Typora\typora-user-images\image-20201214154255754.png)

### 面向对象特征之三：多态

多态性，是面向对象中最重要的概念，在java中有两种体现

	1. 方法的重载（overload）和重写（overwrite）
 	2. 对象的多态性 -- 可以直接应用在抽象类和接口上

java引用变量有两个类型：**编译时类型**和**运行时类型**。编译时类型由申明该变量时使用的类型决定，运行时类型由实际赋给该变量的对象决定。

 1. 若编译时类型和运行时类型不一致，就出现多态（Polymorphism）

    （对象的多态）

对象的多态： 在java中，子类的对象可以替代父类的对象使用

	1. 一个变量只能有一种确定的数据类型
 	2. 一个引用类型变量可能指向（引用）多种不同类型的对象

```java
Person p = new Student();
Person e = new Student(); //Person类型的变量e，指向Student类型的对象
```

子类可看做是特殊的父类，所以父类类型的引用可以指向子类的对象：向上转型（upcasting）

* 一个引用类型变量如果声明为父类的类型，但实际引用的事子类对象，那么该变量就不能再访问子类中添加的属性和方法。

  ```java
  Student m = new Student();
  m.school = "school"; //合理，Student类有school
  
  Person e = new Student();
  e.school = "school";  //非法，Person类没有school成员变量
  //属性是在编译时确定的，编译时e为Person类型，没有school成员变量，因而编译报错。
  
  ```

* 虚拟方法调用（Virtual Method Invocation）

  * 正常的方法调用

    ```java
    Person p = new Person();
    p.getInfo();
    Student s = new Student();
    s.getInfo();
    ```

  * 虚拟方法调用（多态情况下）

    ```java
    Person e = new Student();
    e.getInfo();  //调用Student类的getInfo（）方法
    ```

  * 编译时类型和运行时类型

  编译e时为Person类型，而方法的调用时在运行时确定的，所以调用的是Student类的getInfo（）方法。-----动态绑定

#### 小结

* 前提：
  * 需要存在继承或者实现关系
  * 要有覆盖操作（重写）
* 成员方法：
  * 编译时：要查看引用变量所属的类中是否有所调用的方法。
  * 运行时：调用实际对象所属的类中的重写方法。
* 成员变量：
  * 不具备多态性，只看引用变量所属的类。
* 子类继承父类
  * 若子类重写了父类方法，就意味着子类里定义的方法彻底覆盖了父类里的同名方法，系统将不可能把父类里的方法转移到子类中
  * 对于实例变量则不存在这样的现象，即使子类里定义了与父类完全相同的实例变量，这个实例变量依然不可能覆盖父类中定义的实例变量

#### instanceof操作符

 x   instanceof A

检测x是否为类A的对象，返回值为boolean型；

### Object类、包装类

* Object类是所有java类的根父类
* 如果再类的声明中未使用 extends关键字指明其父类，则默认父类就是Object类。

| No   | 方法名称                            | 类型 | 描述                                       |
| ---- | ----------------------------------- | ---- | ------------------------------------------ |
| 1    | public Object()                     | 构造 | 构造方法                                   |
| 2    | public boolean equals（Object obj） | 普通 | 对象比较                                   |
| 3    | public lnt hashCode（）             | 普通 | 取得Hash码                                 |
| 4    | public String toString（）          | 普通 | 对象打印时调用<br />（返回对象的内存地址） |

#### Object类

##### 对象类型转换（Casting）

* 基本数据类型的Casting

  * 自动类型转换： 小的数据类型可以自动转换成大的数据类型

    如： long g = 20；	double 的= 12.0f

  * 强制类型转换： 可以把大的数据类型强制转换（casting）成小的数据类型

    如：float f = (float)12.0;  int a = (int)1200L;

* 对java对象的强制类型转换称为造型

  * 从子类到父类的类型转换可以自动进行
  * 从父类到子类的类型转换必须通过造型（强制类型转换）实现
  * 无继承关系的引用类型间的转换是非法的

##### equals、==

对于对象来说特殊的类，如String、File、Date，使用 == 毕竟的是对象（对象内存地址），

equals比较的是内容

除了特殊的类之外的其他普通的类的对象，==和equals比较的都是对象（对象内存地址）

如果你想改变某个类的equals，不想用equals比较对象的内存地址，就需要重写equals方法

##### String对象的创建

1. 字面量创建String对象（省内存）

   ```java
   String s1 = "abc";//常量池中添加“abc”对象，返回引用地址给s1对象
   String s2 = "abc";//通过equals()方法判断常量池中已有值为abc的对象，返回相同的引用
   System.out.println(s1 == s2) //true   所以 s1 == s2
   ```

2. new创建String对象

   ```java
   String s3 = new String("def");//在常量池中添加“def”对象，在堆中创建值为“def”的对象s3，返回指向堆中s3的引用
   String s4 = new String("def");//常量池中已有值为“def”的对象，不做处理，在堆中创建值为“def”的对象s4，返回指向堆中s4的引用
   ```

#### 包装类

基本数据类的包装类  ---  基本数据类型与字符串直接的转化！！！

* 针对八种基本定义响应的引用类型-包装类（封装类）
* 有了类的特点，就可以调用类中的方法

| 基本数据类型 | 包装类        |
| ------------ | ------------- |
| boolean      | Boolean       |
| byte         | Byte          |
| short        | Short         |
| **int**      | **Integer**   |
| long         | Long          |
| **char**     | **Character** |
| float        | Float         |
| double       | Double        |

* 基本数据类型包装成包装类的实例--装箱

  * 通过包装类的构造器实现：

    ```java
    int i = 500;
    Integer t = new Integer(i);
    ```

  * 还可以通过字符串参数构造包装类对象：

    ```java
    Float f = new Float("4.56");
    Long l = new Long("asdf"); // NumberFormatException
    ```

* 获得包装类对象中包装的基本类型变量 -- 拆箱

  * 调用包装类的 .xxxValue()方法：

    ```java
    boolean b = new Boolean("false").booleanValue();
    Integer i = new Integer(123);
    int i0 = i.intValue();
    ```

* JSK1.5之后，支持自动装箱，自动拆箱。但类型必须匹配

  ```java
  Integer i1 = 122;//自动装箱
  int i2 = i1;//自动拆箱
  
  Boolean b1 = true;
  boolean b2 = b1;
  ```



* 字符串转换成基本数据类型

  * 通过包装类的构造器实现：

    ```java
    int i = new Integer("12");
    ```

  * 通过包装类的parseXxx静态方法

    ```java
    Float f = Float.parseFloat("12.1");
    int i = Integer.parseInt("1");
    Boolean b = Boolean.parseBoolean("false");
    ```

* 基本数据类型转换成字符串

  * 调用字符串重载的valueOf()方法

    ```java
    String f = String.valueOf(2.34f);
    String i = String.valueOf(i);
    String b = String.valueOf(true);
    ```

  * 更直接的方式

    ```java
    String intStr = 5 + "";
    ```

  

* 包装类用法举例

  装箱：包装类使得一个基本数据类型的数据变成了类。有了类的特点，可以调用类中的方法。

  父类Object的toString方法就输出当前对象的内存地址

  如果要是想要输出类的其他信息，重写toString方法。

  ```java
  int i = new Integer("123");
  i.toString();//对象的内存地址 //
  i  //默认输出 相当于执行 .toString
  ```

  



## 高级类特性2

### 关键字：static

静态的

类变量：如果想让一个类的所有实例共享数据，就用**类变量**;也可以叫**静态变量**

实例变量：只有实例化之后才能使用，属于实例化对象的一部分

```java
public class Chinese{
    static String country; //类变量
     
    String name;  //实例变量
    int age;	  //实例变量
    
}

public class Utils{
    public static String isString(){
        return "string"
    }
}
```



类属性、类方法的设计思想

1. 类属性作为该类各个对象之间共享的变量。**在设计类时，分析哪些类属性不因对象的不同而改变，将这些属性设置为类属性。相应的方法设置为类方法**
2. 如果方法与调用者无关，则这样的方法通常被声明为类方法，由于不需要创建对象就可以调动类方法，从二简化了方法的调用。

类方法，也就是静态方法，工具类（用的多）



staitc 使用范围：在java类中，可用static修饰属性、方法、代码块、内部类

被修饰后的成员具备以下特点：

1. 随着类的加载而加载

 	2.	优先于对象存在
 	3.	修饰的成员，被所有对象所共享
 	4.	访问权限允许时，可不创建对象，直接被类调用

### 理解main方法的语法

由于java虚拟机徐亚红调用类的main（）方法，所以该方法的访问权限必须是public，又因为java虚拟机再执行main（）方法时不必创建对象，所以该方法必须是static的，该方法接受一个String类型的数组参数，该数组中保存执行java命令时传递给所有运行的类的参数

doc命令

```DOS
javac TestMain.java
java TestMain abc 123 lsd 3kd
```



### 类的成员之四：初始化块

1. 初始化块（代码块）作用：
   1. 对java对象进行初始化
2. 程序的执行顺序：
   1. 声明成员变量的默认值
   2. 显示初始化、多个初始化块依次被执行（同级别下按先后顺序执行）
   3. 构造器再对成员进行赋值操作

```java
public class Person {
    String name;
    public Person(){
        this.name = "liuzheng";
        System.out.println("执行的是构造方法");
    }

    //非静态代码块
    {
        System.out.println("执行的是非静态代码块");
    }
}

//执行的是非静态代码块
//执行的是构造方法
```



静态代码块只执行一次

1. 一个类中初始化块若有修饰符，则只能被static修饰，称为静态代码块（static block），当类被载入时，类属性的声明和静态代码块先后顺序被执行，且只被执行依次。
2. static块通常用于初始化static（类）属性

```java
//静态代码块
{
    age = 18;
    showAge();
    System.out.println("执行的是静态代码块");
}
public static void showAge(){
    System.out.println(age);
}
```



* 非静态代码块：没有static修饰的代码块
  * 可以有输出语句
  * 可以对类属性声明进行初始化操作
  * 可以调用静态和非静态的变量或方法
  * 若有多个非静态的代码块，那么按照从上到下的顺序依次执行
  * 每次创建对象的时候，都会执行一次。且先于构造器执行
* 静态代码块：用static修饰的代码块
  * 可以有输出语句
  * 可以对类属性声明进行初始化操作
  * 不可以对非静态的属性初始化。即：不可以调用非静态的属性和方法
  * 若有多个静态的代码块，那么按照从上到下的顺序依次执行
  * 静态代码块的执行要先于非静态代码块
  * 静态代码块只执行一次



```java
//构建了一个没有类名的Person子类  也就是匿名的Person的子类
Person p = new Person(){
    @Override
    public String toString() {
        return super.toString();
    }
    {
        super.name = "sss"
    }
};
//这种类没有类名，就不能显示的new的方法创建对象，如果要是还要再构造器中初始化属性就没有办法了，这样情况就要用代码块来干初始化的工作
```

### 关键字：final

在java中声明类、属性和方法时，可使用关键字final来修饰，表示“最终”

1. final标记的类不能被继承。提高安全性，提高程序的可读性。

2. final标记的方法不能被子类重写

3. final标记的变量（成员变量或局部变量）即称为常量。名称大写，且只能被赋值一次

   1. final标记的成员变量必须在声明的同时或在每个构造方法中或代码块中显示赋值，然后才能使用。

   final double PI = 3.14

### 抽象类（abstract class）



### 更彻底的抽象：接口（interface）

### 类的成员之五：内部类



### 设计模式

#### 单例（Singleton）设计模式

只有一个实例（实例化对象）

在整个软件系统运行过程中，这个类只被实例化一次，以后不论在哪都只调用这一个实例。

什么情况下？

**例如：实例化对象的创建要消耗大量时间和资源。**

解决什么问题？一般都是new对象太费劲



区别是对象什么时候创建的

##### 饿汉式单例模式

最开始，new一个对象，以后所有调用我的都用这个对象

##### 懒汉式单例模式

最开始，对象是null，直到第一个人调用我，才new一个对象，以后所有调用我的都用这个对象

