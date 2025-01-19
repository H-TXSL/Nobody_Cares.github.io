# Java
# 目录
> [Java基础](#Java基础)
> [面相对象编程](#面相对象编程)
> 
## Java基础
### 1. Java基本结构
```Java
// 特殊的多行注释，以/**开头，以*/结束，如果有多行，每行通常以星号开头
/**
 * 可以用来自动创建文档的注释
 */
public class Hello {
    public static void main(String[] args) {
        // 向屏幕输出文本:
        System.out.println("Hello, world!");
        // 单行注释
        /* 多行注释开始
        注释内容
        注释结束 */
    }
} // class定义结束
```
> Java入口程序规定的方法必须是静态方法，方法名必须为main，括号内的参数必须是String数组。

类名要求:
- 类名必须以英文字母开头，后接字母，数字和下划线的组合
- 习惯以大写字母开头
方法名要求:
- 命名和class一样，但是首字母小写
### 2. 变量和数据类型
基本数据类型

| 类型 | 说明 |
| :--: | :--: |
| 整数类型 | byte，short，int，long(long型的结尾需要加L) |
| 浮点数类型 | float(float型结尾加f)，double |
| 字符类型 | char |
| 布尔类型 | boolean | 
| 引用类型 | String |

科学计数法： double d = 4.9e-324; // 科学计数法表示的4.9x10^-324
- 常量： final修饰的变量
- 自动推断变量的类型: var
### 3. 运算
- 求余运算使用%
- 简写的运算符，即+=，-=，*=，/=
```Java
n += 100; // 3409, 相当于 n = n + 100;
n -= 100; // 3309, 相当于 n = n - 100;
```
- 自增++ 自减--
```Java
int n = 3300;
n++; // 3301, 相当于 n = n + 1;
n--; // 3300, 相当于 n = n - 1;
```
- 移位运算
```Java
int n = 7;       // 00000000 00000000 00000000 00000111 = 7
int a = n << 1;  // 00000000 00000000 00000000 00001110 = 14
int b = n << 2;  // 00000000 00000000 00000000 00011100 = 28
int c = n << 28; // 01110000 00000000 00000000 00000000 = 1879048192
int d = n << 29; // 11100000 00000000 00000000 00000000 = -536870912
```
左移29位时，由于最高位变成1，因此结果变成了负数
```Java
int n = 7;       // 00000000 00000000 00000000 00000111 = 7
int a = n >> 1;  // 00000000 00000000 00000000 00000011 = 3
int b = n >> 2;  // 00000000 00000000 00000000 00000001 = 1
int c = n >> 3;  // 00000000 00000000 00000000 00000000 = 0
```
如果对一个负数进行右移，最高位的1不动，结果仍然是一个负数
```Java
int n = -536870912;
int a = n >> 1;  // 11110000 00000000 00000000 00000000 = -268435456
int b = n >> 2;  // 11111000 00000000 00000000 00000000 = -134217728
int c = n >> 28; // 11111111 11111111 11111111 11111110 = -2
int d = n >> 29; // 11111111 11111111 11111111 11111111 = -1
```
无符号的右移运算，使用>>>
它的特点是不管符号位，右移后高位总是补0
因此，对一个负数进行>>>右移，它会变成正数，原因是最高位的1变成了0
```Java
int n = -536870912;
int a = n >>> 1;  // 01110000 00000000 00000000 00000000 = 1879048192
int b = n >>> 2;  // 00111000 00000000 00000000 00000000 = 939524096
int c = n >>> 29; // 00000000 00000000 00000000 00000111 = 7
int d = n >>> 31; // 00000000 00000000 00000000 00000001 = 1
```
对byte和short类型进行移位时，会首先转换为int再进行位移
左移实际上就是不断地×2，右移实际上就是不断地÷2
- 位运算
位运算是按位进行与、或、非和异或的运算
    + & 与运算的规则是，必须两个数同时为1，结果才为1
    + | 或运算的规则是，只要有一个数为1，结果就为1
    + ^ 异或运算的规则是，只要两个数不同，结果就为1
    + ~ 非运算的规则是，0变成1，1变成0
- 三元运算符b ? x : y
判断b是否为true，如果为true，则返回x，否则返回y
### 4. 字符和字符串
- 字符类型char
可以直接用转义字符\u+Unicode编码来表示一个字符
```Java
// 注意是十六进制:
char c3 = '\u0041'; // 'A'，因为十六进制0041 = 十进制65
char c4 = '\u4e2d'; // '中'，因为十六进制4e2d = 十进制20013
```
- 字符串类型String
字符串类型String是引用类型
    + 可以使用+连接任意字符串和其他数据类型
    + 多行字符串
    ```Java
    String s = "first line \n"
         + "second line \n"
         + "end";
    ```
    从Java 13开始，字符串可以用"""..."""表示多行字符串
    ```Java
            // 多行字符串
    public class Main {
        public static void main(String[] args) {
            String s = """
                    SELECT * FROM
                        users
                    WHERE id > 100
                    ORDER BY name DESC
                    """;
            System.out.println(s);
            // 上述多行字符串实际上是5行
            // 最后一个DESC后面还有一个\n
        }
    }
    ```
    多行字符串的排版不规则,总是以最短的行首空格为基准
- 常见的转移字符
```Java
\" 表示字符"
\' 表示字符'
\\ 表示字符\
\n 表示换行符
\r 表示回车符
\t 表示Tab
\u#### 表示一个Unicode编码的字符

String s = "ABC\n\u4e2d\u6587"; // 包含6个字符: A, B, C, 换行符, 中, 文
```
- 空值null
引用类型的变量可以指向一个空值null，它表示不存在，即该变量不指向任何对象
```Java
String s1 = null; // s1是null
String s2 = s1; // s2也是null
String s3 = ""; // s3指向空字符串，不是null
```
### 5. 数组
- 数组操作
数组本身是引用类型
```Java
// 数组所有元素初始化为默认值，整型都是0，浮点型是0.0，布尔型是false
// 数组一旦创建后，大小就不可改变
int[] ns = new int[5]; // 创建一个int类型的数组，长度为5
int size = ns.length; // 数组长度为5
int[] ns2 = new int[] { 68, 79, 91, 85, 62 }; // 直接指定初始化元素
int[] ns3 = { 68, 79, 91, 85, 62 }; // 直接指定初始化元素，省略new int[]

// 快速打印数组内容: Arrays.toString()
// 需要导入java.util.Arrays
System.out.println(Arrays.toString(ns2));
// [68, 79, 91, 85, 62]

// 数组排序: Arrays.sort()
// 导入java.util.Arrays
Arrays.sort(ns2);
System.out.println(Arrays.toString(ns2));
// [62, 68, 79, 85, 91]

```
- 多维数组
```Java
// 二维数组
public class Main {
    public static void main(String[] args) {
        int[][] ns = {
            { 1, 2, 3, 4 },
            { 5, 6, 7, 8 },
            { 9, 10, 11, 12 }
        };
        int[] arr0 = ns[0];
        System.out.println(arr0.length); // 4
    }
}
// 在内存中，结构如下：
            arr0 ─────┐
                      ▼
                    ┌───┬───┬───┬───┐
         ┌───┐  ┌──▶│ 1 │ 2 │ 3 │ 4 │
ns ─────▶│░░░│──┘   └───┴───┴───┴───┘
         ├───┤      ┌───┬───┬───┬───┐
         │░░░│─────▶│ 5 │ 6 │ 7 │ 8 │
         ├───┤      └───┴───┴───┴───┘
         │░░░│──┐   ┌───┬───┬───┬───┐
         └───┘  └──▶│ 9 │10 │11 │12 │
                    └───┴───┴───┴───┘
System.out.println(ns[1][2]); // 7

// 打印二维数组: Arrays.deepToString()
// 导入java.util.Arrays
System.out.println(Arrays.deepToString(ns));
// [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]]

三维数组
int[][][] ns2 = {
    {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    },
    {
        {10, 11},
        {12, 13}
    },
    {
        {14, 15, 16},
        {17, 18}
    }
};
// 它在内存中的结构如下：
                              ┌───┬───┬───┐
                   ┌───┐  ┌──▶│ 1 │ 2 │ 3 │
               ┌──▶│░░░│──┘   └───┴───┴───┘
               │   ├───┤      ┌───┬───┬───┐
               │   │░░░│─────▶│ 4 │ 5 │ 6 │
               │   ├───┤      └───┴───┴───┘
               │   │░░░│──┐   ┌───┬───┬───┐
        ┌───┐  │   └───┘  └──▶│ 7 │ 8 │ 9 │
ns ────▶│░░░│──┘              └───┴───┴───┘
        ├───┤      ┌───┐      ┌───┬───┐
        │░░░│─────▶│░░░│─────▶│10 │11 │
        ├───┤      ├───┤      └───┴───┘
        │░░░│──┐   │░░░│──┐   ┌───┬───┐
        └───┘  │   └───┘  └──▶│12 │13 │
               │              └───┴───┘
               │   ┌───┐      ┌───┬───┬───┐
               └──▶│░░░│─────▶│14 │15 │16 │
                   ├───┤      └───┴───┴───┘
                   │░░░│──┐   ┌───┬───┐
                   └───┘  └──▶│17 │18 │
                              └───┴───┘
// ns2[1][1][1] = 13
```

### 6. 输入输出和条件循环语句
- 输入和输出
println()会自动添加换行符，而print()不会
    + 格式化输出
    ```Java
        // 格式化输出
    public class Main {
        public static void main(String[] args) {
            double d = 3.1415926;
            System.out.printf("%.2f\n", d); // 显示两位小数3.14
            System.out.printf("%.4f\n", d); // 显示4位小数3.1416
        }
    }
    ```
    + 占位符

    | 占位符 | 说明 |
    | :--: | :--: |
    | %d | 格式化输出整数 |
    | %x | 格式化输出十六进制整数 |
    | %f | 格式化输出浮点数 |
    | %e | 格式化输出科学计数法表示的浮点数 |
    | %s | 格式化字符串 |

    连续两个%%表示一个%字符本身

    ```Java
        // 格式化输出
    public class Main {
        public static void main(String[] args) {
            int n = 12345000;
            System.out.printf("n=%d, hex=%08x", n, n); // 注意，两个%占位符必须传入两个数
            // n=12345000, hex=00bc5ea8
        }
    }
    ```
    详细的格式化参数请参考JDK文档[java.util.Formatter](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Formatter.html#syntax)
- 输入
```Java
// 通过import语句导入java.util.Scanner，import是导入某个类的语句，必须放到Java源代码的开头
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in); // 创建Scanner对象
        System.out.print("Input your name: "); // 打印提示
        String name = scanner.nextLine(); // 读取一行输入并获取字符串
        System.out.print("Input your age: "); // 打印提示
        int age = scanner.nextInt(); // 读取一行输入并获取整数
        System.out.printf("Hi, %s, you are %d\n", name, age); // 格式化输出
    }
```
- 判断
```Java
// if else
if () {

} else {

}
// else if 
if () {

} else if {

} else {

}
```
> 判断引用相等用==，判断内容相等用equals()

```Java
// 执行s1.equals(s2)时，如果变量s1为null，会报NullPointerException
// 要避免NullPointerException错误，可以利用短路运算符&&
// 条件判断
public class Main {
    public static void main(String[] args) {
        String s1 = null;
        if (s1 != null && s1.equals("hello")) {
            System.out.println("hello");
        }
    }
}
```  
- switch语句
```Java
// switch
public class Main {
    public static void main(String[] args) {
        String fruit = "apple";
        switch (fruit) {
        case "apple":
            System.out.println("Selected apple");
            break;
        case "pear":
            System.out.println("Selected pear");
            break;
        case "mango":
            System.out.println("Selected mango");
            break;
        default:
            System.out.println("No fruit selected");
            break;
        }
    }
}
```

> 从Java 12开始，switch语句升级为更简洁的表达式语法，使用类似模式匹配（Pattern Matching）的方法，保证只有一种路径会被执行，并且不需要break语句。

```Java
// switch
// 新语法使用->，如果有多条语句，需要用{}括起来。不要写break语句，因为新语法只会执行匹配的语句，没有穿透效应
public class Main {
    public static void main(String[] args) {
        String fruit = "apple";
        switch (fruit) {
        case "apple" -> System.out.println("Selected apple");
        case "pear" -> System.out.println("Selected pear");
        case "mango" -> {
            System.out.println("Selected mango");
            System.out.println("Good choice!");
        }
        default -> System.out.println("No fruit selected");
        }
    }
}

// 使用新的switch语法，不但不需要break，还可以直接返回值
// switch
public class Main {
    public static void main(String[] args) {
        String fruit = "apple";
        int opt = switch (fruit) {
            case "apple" -> 1;
            case "pear", "mango" -> 2;
            default -> 0;
        }; // 注意赋值语句要以;结束
        System.out.println("opt = " + opt);
    }
}

// 如果需要复杂的语句，我们也可以写很多语句，放到{...}里，然后，用yield返回一个值作为switch语句的返回值

// yield
public class Main {
    public static void main(String[] args) {
        String fruit = "orange";
        int opt = switch (fruit) {
            case "apple" -> 1;
            case "pear", "mango" -> 2;
            default -> {
                int code = fruit.hashCode();
                yield code; // switch语句返回值
            }
        };
        System.out.println("opt = " + opt);
    }
}
```
- while循环
```Java
while (条件表达式) {
    循环语句
}
// 继续执行后续代码
```
- do...while循环
```Java
do {
    执行循环语句
} while (条件表达式);
```
- for循环
```Java
for (初始条件; 循环检测条件; 循环后更新计数器) {
    // 执行语句
}
// for循环还可以缺少初始化语句、循环条件和每次循环更新语句

// for each循环
public class Main {
    public static void main(String[] args) {
        int[] ns = { 1, 4, 9, 16, 25 };
        for (int n : ns) {
            System.out.println(n);
        }
    }
}
```
- break 会跳出当前循环，也就是整个循环都不会执行了。
- continue 则是提前结束本次循环，直接继续执行下次循环
## 面相对象编程
