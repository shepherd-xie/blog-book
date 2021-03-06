## Java方法的定义及使用

---

关于方法（method）的定义：（引用自[维基百科](https://zh.wikipedia.org/wiki/方法_(電腦科學))）

> 在面向对象程序设计中，方法（英语：method）指的是类别（所谓的类方法、静态方法或工厂方法）、或者是对象（所谓的实例方法）两者其中之一的一种子程序。如同过程化编程语言的程序，一个方法通常以一系列的语句所组成，并以之完成一个动作。其可以借由输入一组参数以制订所需的动作，且一部分的方法可能会有输出值（所谓的返回值）。方法的目的是提供一个机制，以访问（对于读和写）对象或类别的私有数据存储区。

### 方法的基本概念

所谓方法，就是一段可以被重复调用的代码段，利用此操作可以封装执行的代码。

但是在 Java 之中，方法的定义格式比较复杂，所以本次给出的方法有一个要求：值的是定义在主类之中，并且由主方法直接调用的方法，所以现在给出的方法创建语法：

```java
public static 返回值类型 方法名称(参数类型 参数名称,...) {
    方法体;    //被重复调用的一段代码
    [return [返回值];]
}
```

在本定义格式之中，方法有一个返回值类型，指的是这个方法返回结果，对于此类的类型可以有两种：

* 直接设置 Java 中的数据类型（基本数据类型，引用数据类型），如果方法设置了返回值，那么必须使用 return 语句返回与之数据类型对应的数据；
* 方法没有返回值：void，可以不使用 return 返回内容，但是可以使用 return 结束方法调用。

在定义方法名称的时候也是有命名要求的：第一个单词的首字母小写，而后每个单词的首写字母大写（小驼峰式命名法）。

> 1、小驼峰式命名法（lower camel case）：
>
> 第一个单字以小写字母开始，第二个单字的首字母大写。例如：firstName、lastName。
>
> 2、大驼峰式命名法（upper camel case）：
>
> 每一个单字的首字母都采用大写字母，例如：FirstName、LastName、CamelCase，也被称为 Pascal 命名法。
>
> 补充说明，在 JAVA 中：类名的标识符一般用大驼峰式书写格式，方法和变量的标识符则多用小驼峰式书写格式(关于具体的命名规范可参考[Java编程规范](../README.md)。

**范例：** 定义一个没有参数没有返回值的方法

```java
public static void main(String[] args) {
    printInfo();    //直接调用方法
}
//定义没有参数，没有返回值的方法
public static void printInfo() {
    System.out.println("Hello World !");
}
```

可以发现将若干代码封装在一个方法之中，就可以根据需要重复执行这些方法所定义的代码。实际上是否要形成方法，并没有一个绝对的条件。但是有一点可以作为参考：如果在代码之中你总是在对一些操作进行复制粘贴的时候，就可以考虑将此类代码定义成为方法以供重复调用使用。

**范例：** 定义一个有参数无返回值的方法

```java
public static void main(String[] args) {
    test(90.0);    //直接调用方法
}
//定义有参数，没有返回值的方法
public static void test(double score) {
    if (score >= 90 && score <= 100) {
        System.out.println("优秀");
    } else if (score >= 70 && score < 90) {
        System.out.println("良好");
    } else if (score >= 60 && score < 70) {
        System.out.println("及格");
    } else if (score >= 0 && score < 60) {
        System.out.println("不及格");
    } else {
        System.out.println("不存在的成绩");
    }
}
```

有了参数之后，方法就可以根据不同的参数内容进行数据的处理。

**范例：** 定义有参数有返回值的方法

```java
public static void main(String[] args) {
    //方法的返回值可以进行接收
    int result = add(10, 20);
    System.out.println("计算结果：" + result);
    //也可以将方法返回值进行输出
    System.out.println(add(40, 50));
}
//定义有参数，有返回值的方法
public static int add(int x, int y) {
    return x + y;
}
```

如果说现在一个方法上使用了void定义为它的返回值，那么可以使用return结束一个方法的调用。

**范例：** 利用return结束方法调用

```java
public static void main(String[] args) {
    set(100);
    set(3);
    set(10);
}
//定义有参数，有返回值的方法
public static void set(int x) {
    if (x == 3) {
        return;
    }
    System.out.println("x = " + x);
}
```

只有方法返回值类型为void的前提下才可以使用。

### 方法的重载

如果说有一个方法要执行多项操作，例如add方法，它可能执行两个整数的相加，也有可能执行三个整数的相加，还有可能执行两个小数的相加，那么在这样的情况下，一个方法体肯定无法满足这样的需求，要为add方法轻易多个不同的功能实现，此类操作就成为方法重载，但是在进行方法的重载时要求：方法的名称相同，参数的类型或个数不同。

**范例：** 观察方法重载

```java
public static void main(String[] args) {
    //重载方法执行时会根据传入参数的类型及个数匹配不同的方法体执行
    int result = add(10, 20);
    System.out.println("计算结果：" + result);
    System.out.println(add(40, 50, 60));
}
public static int add(int x, int y) {
    return x + y;
}
public static int add(int x, int y, int z) {
    return x + y + z;
}
public static double add(double x, double y) {
    return x + y;
}
```

**范例：** 观察代码

```java
public static void main(String[] args) {
    System.out.println("hello");    //输出String
    System.out.println(1);        //输出int
    System.out.println(12.3);    //输出double
    System.out.println(true);    //输出bolean
    System.out.println('A');    //输出char
}
```

可以发现“ System.out.println\(\) ”所有的内容都可以执行，所以此方法就是被重载后的方法。

方法重载的概念本身很容易理解，但是对于方法重载有两点说明：

* 在进行方法重载时候一定要考虑到参数类型的统一上，虽然可以实现重载方法返回不同类型的操作，但是从标准的开发来讲，建议所有的重载后的方法使用同一种返回值类型；
* 方法重载的时候是依靠参数的数据类型及个数来区分不同的方法，而不是通过返回值类型来区分的。

### 方法的递归调用

递归调用是迈向数据结构开发的第一步，但是想要熟练地掌握递归调用是需要大量的代码练习。

所谓递归调用指的就是一个方法自己调用自己的情况，但是想要自己调用自己就一定需要一个结束的条件。并且每次调用的时候都要去修改这个结束条件。

之所以在开发之中尽量减少递归操作，是因为如果处理不得当就有可能出现内存的溢出问题。

**范例：** 实现一个1~100的累加操作

```java
int sum = 0;
int current = 1;
while (current <= 100) {
    sum += current;
    current ++;
}
System.out.println(sum);
```

将以上的代码形式转化为递归操作。

**范例：** 递归调用

```java
public static void main(String[] args) {
    sum(100);
}
public static int sum(int num) {
    if (num == 1) {
        return 1;
    }
    return num + sum(num - 1);
}
```



