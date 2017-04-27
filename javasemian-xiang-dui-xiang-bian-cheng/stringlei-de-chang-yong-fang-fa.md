## String类的常用方法

---

String在所有的开发之中都一定要使用到，String类里面提供了一系列的功能操作方法，下面列举出一部分的方法，而对于有一些操作，需要等待全部的知识掌握时候才可以进行学习。

对于系统类的方法，一定要自己去查询文档，对于String类由于开发的过程中使用较多，所以一定要熟记String类中所提供的方法。

对于每一个文档的内容而言，他都有以下的几部分组成：

* 类的定义以及相关的继承结构；
* 类的一些简短的说明；
* 类中的成员组成；
* 类中所提供的构造方法；
* 类中所提供的的普通方法；
* 成员、构造方法、普通方法的详细说明。

### 字符与字符串

很多的语言之中都是利用了字符数组的概念来描述字符串的信息，这一点在String类的方法上也都有所提供。

| No. | 方法名称 | 类型 | 描述 |
| :---: | :---: | :---: | :---: |
| 1 | public String\(char\[\] value\) | 构造 | 将字符数组变为String类对象 |
| 2 | public String\(char\[\] value,int offset,int count\) | 构造 | 将部分字符数组变为String |
| 3 | public char charAt\(int index\) | 普通 | 返回指定索引对应的字符信息 |
| 4 | public char\[\] toCharArray\(\) | 普通 | 将字符串以字符数组的形式返回 |

**范例：**取出指定索引的字符

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "hello";
        char c = str.charAt(0);
        System.out.println(c);
    }
}
```

程序之中字符串的下标都是从0开始的。

**范例：**字符数组与字符串的转换

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "hello";
        char[] data = str.toCharArray();
        for (int i = 0; i < data.length; i ++) {
            System.out.println(data[i]);
        }
    }
}
```

**范例：**将字符串转大写

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "hello";
        char[] data = str.toCharArray();
        for (int i = 0; i < data.length; i ++) {
            data[i] += 'A' - 'a';
        }
        System.out.println(new String(data));
        System.out.println(new String(data, 1, 3));
    }
}
```

**范例：**给定一个字符串，要求判断其是否由数组组成

**思路：**如果整个字符串要判断是不是数字无法实现，但是可以将字符串变为字符数组，而后判断每一个字符的内容是否是数字，如果该字符的范围在（'0'~'9'）指定的范畴之内，那么就是数字。

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "681356486";
        if (isNumber(str)) {
            System.out.println("字符串由数字组成!");
        } else {
            System.out.println("字符串不是由数字组成");
        }
    }
    //判断字符串是否由数字组成
    public static boolean isNumber(String temp) {
        char[] data = temp.toCharArray();
        for (int i = 0; i < data.length; i ++) {
            if (data[i] > '9' || data[i] < '0') {
                return false;
            }
        }
        return true;
    }
}
```

如果写的某一个方法返回的内容是boolean，那么习惯性的做法是将其以“isXxx”进行命名。

### 字节与字符串

字节使用byte描述，使用字节一般主要用于数据的传输或者进行编码转换的时候使用，而咋String类里面就提供有将字符串变为字节数组的操作，目的就是为了传输以及编码转换。

| No. | 方法名称 | 类型 | 描述 |
| :---: | :---: | :---: | :---: |
| 1 | public String\(byte\[\] bytes\) | 构造 | 将全部字节数组变为字符串 |
| 2 | public String\(byte\[\] bytes,int offset,int length\) | 构造 | 将部分字节数组变为字符串 |
| 3 | public byte\[\] getBytes\(\) | 普通 | 将字符串将字符串变为字节数组 |
| 4 | public byte\[\] getBytes\(String charsetName\) throws UnsupportedEncodingException | 普通 | 进行编码转换 |

**范例：**观察字符串与字节数组的转换

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "helloworld";
        byte[] data = str.getBytes(); //将字符串转为字节数组
        for (int i = 0; i < data.length; i ++) {
            data[i] += 'A' - 'a'; //将小写字母变为大写字母
        }
        System.out.println(new String(data));
        System.out.println(new String(data, 5, 5));
    }
}
```

因为现在操作的是英文字母，所以感觉与字符类似。

在以后讲解IO操作的时候会牵扯到字节数组的操作，在后续的开发之中会逐步接触到乱码的处理问题。

### 字符串的比较

如果要进行字符串内容相等的判断使用equals\(\)，但是在String类里面定义的比较判断不止这一个。

| No. | 方法名称 | 类型 | 描述 |
| :---: | :---: | :---: | :---: |
| 1 | public boolean equals\(String anObject\) | 普通 | 进行相等判断，区分大小写 |
| 2 | public boolean equalsIgnoreCase\(String anotherString\) | 普通 | 进行相等判断，不区分大小写 |
| 3 | public int compareTo\(String anotherString\) | 普通 | 判断两个字符串的大小（按照字符编码比较）此方法的返回值有如下三种结果：=0，表示要比较的两个字符串内容相同；&gt;0，表示大于的结果；&lt;0，表示小于的结果。 |

**范例：**相等判断

```java
public class MainClass {
    public static void main(String[] args) {
        String stra = "Hello";
        String strb = "hELLO";
        System.out.println(stra.equals(strb)); //false
        System.out.println(stra.equalsIgnoreCase(strb)); //true
    }
}
```

**范例：**观察compareTo\(\)方法

```java
public class MainClass {
    public static void main(String[] args) {
        String stra = "Hello";
        String strb = "hELLO";
        System.out.println(stra.compareTo(strb));
    }
}
```

现在只有String类的对象才具有大小关系判断。

### 字符串查找

从一个完整的字符串之中要判断某一个子字符串是否存在，这一功能可以使用如下的方法完成。

| No. | 方法名称 | 类型 | 描述 |
| :---: | :---: | :---: | :---: |
| 1 | public boolean contains\(String s\) | 普通 | 判断指定的内容是否存在 |
| 2 | public int indexOf\(String str\) | 普通 | 由前向后查找指定字符串的位置，如果查找到返回第一个字母的索引，如果找不到返回-1。 |
| 3 | public int indexOf\(String str,int fromIndex\) | 普通 | 从指定位置由前向后查找指定字符串，找不到返回-1。 |
| 4 | public int lastIndexOf\(String str\) | 普通 | 由后向前查找指定字符串，找不到返回-1。 |
| 5 | public int lastIndexOf\(String str,int fromIndex\) | 普通 | 从指定位置由后向前查找指定字符串，找不到返回-1. |
| 6 | public boolean startsWith\(String prefix\) | 普通 | 判断是否以指定字符串开头 |
| 7 | public boolean startsWith\(String prefix,int toffset\) | 普通 | 从指定位置开始判断是否以指定字符串开头 |
| 8 | public boolean endsWith\(String suffix\) | 普通 | 判断是否以指定字符串结尾 |

**范例：**使用indexOf\(\)等功能查找

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "helloworld";
        System.out.println(str.indexOf("world"));
        System.out.println(str.indexOf("l"));
        System.out.println(str.indexOf("l", 3));
        System.out.println(str.lastIndexOf("l"));
    }
}
```

以上的过程都只是返回了位置。但是在一些程序之中需要告诉用户的是有没有的结果，最早的做法是判断查询结果是否是“-1”。

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "helloworld";
        if (str.indexOf("world") != -1) {
            System.out.println("可以查询到数据。");
        }
    }
}
```

但是JDK1.5开始之后出现了contains\(\)方法，这个方法可以直接返回boolean。

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "helloworld";
        if (str.contains("world")) {
            System.out.println("可以查询到数据。");
        }
    }
}
```

使用contains\(\)更加的简单，并且在整个Java里面，contains已经成为了一个查询的代名词。

**范例：**开头或结尾判断

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "##@@hello**";
        System.out.println(str.startsWith("##"));
        System.out.println(str.startsWith("@@", 2));
        System.out.println(str.endsWith("**"));
    }
}
```

这些开头和结尾的判断往往可以作为一些标记在程序中出现。

### 字符串替换

指的是使用一个新的字符串替换掉旧的字符串，支持的方法有如下几个：

| No. | 方法名称 | 类型 | 描述 |
| :---: | :---: | :---: | :---: |
| 1 | public String replaceAll\(String **regex**,String replacement\) | 普通 | 用新的内容替换掉全部旧的内容 |
| 2 | public String replaceFirst\(String **regex**,String replacement\) | 普通 | 替换首个满足条件的内容 |

**范例：**观察替换掉的结果

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "helloworld";
        String resultA = str.replaceAll("l", "_");
        String resultB = str.replaceFirst("l", "_");
        System.out.println(resultA);
        System.out.println(resultB);
    }
}
```

对于替换的操作后续还会有更加完善的讲解。

### 字符串截取

从一个完成的字符串之中可以截取部分的子字符串数组，支持的方法如下：

| No. | 方法名称 | 类型 | 描述 |
| :---: | :---: | :---: | :---: |
| 1 | public String substring\(int beginIndex\) | 普通 | 从指定索引截取到结尾 |
| 2 | public String substring\(int beginIndex,int endIndex\) | 普通 | 截取部分子字符串 |

**范例：**验证操作

```java
public class MainClass {
    public static void main(String[] args) {
        String str = "helloworld";
        String resultA = str.substring(5);
        String resultB = str.substring(0, 5);
        System.out.println(resultA);
        System.out.println(resultB);
    }
}
```

### 字符串拆分

将一个完整的字符串，按照指定的内容拆分为字符串数组，方法如下：

| No. | 方法名称 | 类型 | 描述 |
| :---: | :---: | :---: | :---: |
| 1 | public String substring\(int beginIndex\) | 普通 | 从指定索引截取到结尾 |
| 2 | public String substring\(int beginIndex,int endIndex\) | 普通 | 截取部分子字符串 |


