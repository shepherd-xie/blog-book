## Java数据类型划分

---

任何的程序严格来讲都属于一个数据的处理游戏。所以对数据的保存就必须有严格的限制，这些限制的划分就体现在了数据类型上，即：不同的数据类型可以保存不同的数据内容。

Java一共分为两大类数据：基本数据类型、引用数据类型；

* 基本数据类型：
  * 数值型：
    * 整形：byte、short、int、long；_默认值：0_
    * 浮点型：float、double；_默认值：0.0_
  * 字符型：char；_默认值：‘\u0000’_
  * 布尔型：boolean；_默认值：false_
* 引用数据类型：数组、类、接口；_默认值：null_

基本数据类型不牵扯内存分欧问题，而引用数据类型需要由开发者为其分配空间，而后进行关系的匹配。

基本数据类型一共分为八种、引用数据类型一共分为三种。

选择数据类型原则：

* 如果想要表示整数使用int，表示小数使用double；
* 如果描述日期时间数字或者表示文件（或内存）大小使用long；
* 如果要实现内容传递或者是编码转换使用byte；
* 如果要想实现逻辑的控制，可以使用boolean描述；
* 如果想要使用中文，使用char可以避免乱码问题。

| 数据类型 | 大小/位 | 可表示的数据范围 |
| :---: | :---: | :---: |
| long（长整形） | 64 | -9223372036854775808 ~ 9223372036854775807 |
| int（整数） | 32 | -2147483648 ~ 2147483647 |
| short（短整型） | 16 | -32768 ~ 32767 |
| byte（位） | 8 | -128 ~ 127 |
| char（字符） | 16 | 0 ~ 65535 |
| float（单精度） | 32 | -3.4E38 ~ 3.4E38 |
| double（双精度） | 64 | -1.7E308 ~ 1.7E308 |

### 整形

任何一个数字常量（例如：30、100）都属于int类型的数据类型。即：在Java中所有设置的整数内容默认情况下都是int型数据。

**范例：** 整形的定义

```java
//为变量设置内容用如下格式：
//数据类型 变量名称 = 常量；
//所有变量名称在同一块代码中只允许声明一次
int num = 10;     //10是常量，常量的默认类型是int
int result = num * 2;    //利用num变量的内容乘以2，并赋值给result
System.out.println(result);
```

实际上变量与常量最大的区别只有一个：常量的内容是固定的，而变量的内容是可以改变的。

每一种数据类型都有其对应数据类型的保存范围，那么下面来观察一个程序。

**范例：** 观察如果超过了int的最大值或最小值的结果

```java
int max = Integer.MAX_VALUE;     //取出最大值
int min = Integer.MIN_VALUE;     //取出最小值
System.out.println(max);     //2147483647
System.out.println(min);     //-2147483648
// int变量 ± int型常量 = int型数据
System.out.println(max + 1);    //最大值加1：-2147483648
System.out.println(min - 1);    //最小值减1：2147483647
System.out.println(min - 2);    //最小值减2：2147483646
```

任何的数据的计算都是按照二进制进行的，第一位是符号位，其他的31位是数据位。

此种现象称为数据的溢出，那么如果要想解决这种溢出的问题，就只能通过扩大数据范围的方式来实现，比int范围更大的是long数据类型。

**范例：** 扩大数据类型

```java
int max = Integer.MAX_VALUE;     //取出最大值
int min = Integer.MIN_VALUE;     //取出最小值
// int变量 ± long型常量 = long型数据
System.out.println(max + 1L);         //最大值加1：2147483648
System.out.println(min - (long)1);    //最小值减1：-2147483649
// long变量 ± int型常量 = long型数据
System.out.println((long)min - 2);    //最小值减2：-2147483650
```

在程序的世界里面，数据类型的转换有以下规律：

* 数据范围小的数据与数据范围大的数据进行数学计算的时候，自动向大的范围的数据类型转换后计算；
* 数据范围大的数据要变为数据范围小的数据，必须采用强制转换；
* 如果是常量进行强制转换，有两种形式：常量_标记（L，l）、_使用“（数据类型）”。

现在为止计算结果是正确的，所以想要成功的解决数据溢出，一定要使用更大的数据范围。

只要写的代码属于正常可以使用的代码，一般不会发生数据溢出的情况。

以上的代码是利用了数据的转型解决了数据的操作错误，但是对于程序而言，除了可以把数据范围小的数据类型转化成数据范围大的数据类型之外，也可以将数据范围大的数据类型转化成数据范围小的数据类型，就必须使用“（数据类型）”的格式。

**范例：** 将范围大的数据类型变为范围小的数据类型

```java
long num = 1000;         //1000常量是int型，使用long接收，发生了向大范围转型的操作
int x = (int)num;        //把long变为int
System.out.println(x);   //1000
```

如果将long变为了int时所保存的数据超过了int的范围，那么依然会出现数据溢出。

```java
long num = 2147483649L;
int x = (int)num;        //把long变为int
System.out.println(x);   //-2147483647
```

**注意：区分以下情况（数字1与小写字母l）**

```java
System.out.println(11 + 1l);
System.out.println(11 + 11);
```

在整型数据之中，byte型数据是一个非常有用处的数据类型，首先对于byte型数据它的取值范围：-128 ~ 127之间。

**范例：** 观察byte转换

```java
int num = 130;         //超过了byte的范围
byte x = (byte)num;    //由int变为byte
System.out.println(x); //-126
```

但是由于byte使用的特殊性，Java对其有一些很好的改善。

**范例：** 观察byte操作

```java
byte num = 100;
System.out.println(num);
```

虽然任何一个整数都属于int型，但是java编译的时候，如果发现使用的数据变量类型为byte，并且设置的内容在byte数据范围之内，那么就会自动的实现数据转型。如果超过了，则依然会以int型为主。

**提示：**所有的变量在使用的时候一定不要去相信默认值，都要设置具体内容。

如果在方法中定义的默认值是不起任何作用的。标准的做法是在定义变量时设置默认值。

```java
int num = 0;
System.out.println(num);
```

### 浮点数

浮点数就是小数，Java中只要是小数，那么对应的就是double型数据（double是保存范围最广的数据类型）。

**范例：** 定义douoble型变量

```java
//10.2是一个小数所以属于double型
double num = 10.2;
//double型 * int型（转化为double，2.0） = double型
System.out.println(num * 2);
```

由于默认的小数类型就是double，所以如果使用了float表示需要将double型变为float型，需要采用强制转换。

**范例：** 使用float型

```java
float f1 = 10.2F;
float f2 = (float)10.2;
System.out.println(f1 * f2); //104.03999
```

但是发现最终的结果有一点问题，变成了“104.03999”。这个问题如果追溯起来，从JDK1.0的时候就存在这个bug，解决不了，只能通过后期的处理完成。（可以参考数据是如何在内存中存储的）

实际上最早开发的时候，考虑到内存的问题，往往能使用float就不使用double，例如：J2ME开发的时候，由于内存苛刻，所以往往会压缩数据范围，以节约空间。现在随着硬件成本的降低，所以是否使用double和float区别意义就不大了，就直接double数据即可。

需要注意的是，所有的数据类型只有double才可以保存小数，那么观察下面的代码：

```java
int x = 9;
int y = 5;
System.out.println(x / y);
```

此时如果进行了除法计算发现最终的计算结果变为了1，因为所有的小数位被忽略了。此时要想得出正确的计算结果，则可以将其中的一个整形变为浮点型。

```java
int x = 9;
int y = 5;
System.out.println((double)x / y);
```

在以后的开发中，一定要考虑到整形不保留小数位的问题。

### 字符型：char

byte是属于字节，按照传统的概念来讲，一个字符=2个字节，对于字符除了与字节有一些关系之外，最主要的关系在于与int型变量的转换。

在计算机的世界里面一切都是编码的形式出现的，Java使用的是十六进制的UNICODE编码，此类编码可以保存任意的文字，但是这个编码在设计的过程中，考虑到与其他语言的结合问题（C/C++），在此编码里面包含了ASCII码的部分编码。

在程序之中使用 “ ' ” 声明的内容称为字符。每一个单引号里面只能保存一位字符。

**范例：** 定义字符

```java
char c = 'A'; //字符
//字符可以和int型互相转换（以编码的形式出现）
int num = c;
System.out.println(c);
System.out.println(num);
```

经过测试发现一些编码情况：

* 'A'（65） ~ 'Z'（90）
* 'a'（97） ~ 'z'（122）
* '0'（48） ~ '9'（57）

其中“A”的编码值要小于“a”的编码值32，就可以利用简单的数学计算来实现大小写转换。

**范例：** 实现转换过程

```java
char c = 'A'; //大写字母
int num = c; //需要将字符变为int型才可以使用加法计算
num = num + 32; //变为小写字母的编码
c = (char)num; //将int变为char型
System.out.println(c);
```

或者

```java
char c = 'A'; //大写字母
c = c + ('a' - 'A'); //小写与大写之间的差值
System.out.println(c);
```

传统的编程语言中，字符里面只能够保存一些英文字母的标记，但是在Java之中，由于使用了UNICODE编码，这种十六进制的编码可以保存任意的文字，可以设置一个中文字符。

```java
char c = '陈';
int num = c;
System.out.println(num);
```

正因为现在的中文保存的方便，所以在处理断句的时候很好用。

只有在处理中文的时候，字符数据才有那么一点点的帮助，其他的情况下，几乎用不到字符数据。

### 布尔型

布尔是一个数学家的名字，布尔型是一种逻辑结果，主要保存两类数据：true、false，这类数据主要用于一些程序的逻辑使用上。

**范例：** 定义boolean型

```java
//布尔只有两种取值：true、false
boolean flag = true;
if (flag) {
    System.out.println("Hello World!");
}
```

在许多的语言之中，由于设计的初期没有考虑到布尔型的问题，那么就使用了数字0表示false，而非数字0表示true，但是这样的设计对于代码比较混乱，Java里面不允许使用0或1填充布尔型数据变量内容。

### String型数据

只要是项目开发，100%会使用String。但是与其他几种基本数据类型相比，String属于引用数据类型（它属于一个类，在Java里面只要是类名称，每一个单词的首字母都是大写的），但是这个类是用的比较特殊。

String表示的是一个字符串，即：多个字符的集合，String要求使用“ " ”声明其内容。

**范例：** 观察String操作

```java
String str = "Hello World !";
System.out.println(str);             //字符串变量
System.out.println("Hello World !"); //字符串常量
```

在String操作里面，也可以使用“ + ”进行字符串的连接操作。

**范例：** 字符串连接

```java
String str = "Hello";
str = str + " World !";
System.out.println(str);
```

> 此处的“ + ”实际上只是一个[语法糖（Syntactic sugar）](https://zh.wikipedia.org/wiki/%E8%AF%AD%E6%B3%95%E7%B3%96)，当“ + ”的左右两侧出现String类型数据时底层调用的是[String::concat](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#concat-java.lang.String-)来实现字符串拼接。

数学计算里面有“ + ”，字符串里面也有“ + ”，如果一起使用呢？

```java
int numA = 100;
double numB = 99.0;
String str = "加法计算：" + numA + numB;
System.out.println(str);
```

从之前学习的数据类型来说，任何的数据类型都向范围大的数据类型进行转换，那么如果是int和double，int应该先变为double，而后进行加法计算，但是如果遇见了String，那么一切都变了，可以简单理解为，所有的数据类型如果遇见了String的“ + ”，那么所有的数据类型都先变为String型数据，而后再执行字符串的连接操作，那么自然结果是错的，此时只有通过“ \(\) ”来改变计算结果。

```java
int numA = 100;
double numB = 99.0;
String str = "加法计算：" + (numA + numB);
System.out.println(str);
```

先执行括号内的加法计算，而后再讲结果与字符串进行连接。

在Java里面也支持多种转义字符的使用，例如：换行（\n）、制表符（\t）、\（\）、双引号（\"）、单引号（\'）。

**范例：** 转义字符

```java
String str = "Hello \n\t\"World\"";
System.out.println(str);
```

这些转义字符在Java的学习过程之中考虑到格式显示经常会出现。

