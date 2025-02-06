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
#### 字符类型char
可以直接用转义字符\u+Unicode编码来表示一个字符
```Java
// 注意是十六进制:
char c3 = '\u0041'; // 'A'，因为十六进制0041 = 十进制65
char c4 = '\u4e2d'; // '中'，因为十六进制4e2d = 十进制20013   
```
#### 字符串类型String
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
+ 字符串的不可变性
    字符串是不可变对象，字符串本身的值是不能改变的
```Java
String s = "Hello";
s = "hi"; // 把s指向的字符串"Hello"改成了"hi"
```
字符串的不变性是指引用永远指向同一个字符串，对字符串的修改实际上是创建了一个新的字符串对象，并且让引用指向这个新的字符串
```Java
String str1 = "123"; 
// 将 str1 的引用赋值给 str2，此时 str1 和 str2 都指向同一个字符串对象 "123"
String str2 = str1; 
// 将 str2 的引用修改为指向新的字符串对象 "345"
str2 = "345"; 
System.out.println(str1); // 输出 "123"
```
在 Java 中，对于 String 类型，由于其不可变性，修改一个引用不会影响其他引用，除非使用可变的字符串类如 StringBuilder 或 StringBuffer
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
#### 输入和输出
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
#### if判断
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
#### switch语句
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
#### while循环
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
### 1. 面向对象基础
```Java
// 定义类名为Student的class
public class Student {
    // 字段
    public String name;
    public int age;
    private String gender; // private修饰，外部无法访问

    // 构造函数
    // 构造方法的名称就是类名
    // 构造方法没有返回值（也没有void），调用构造方法，必须用new操作符
    // 一个类没有定义构造方法，编译器会自动为我们生成一个默认构造方法，它没有参数，也没有执行语句
    // 无参构造函数
    public Student() {}

    // 如果我们自定义了一个构造方法，那么，编译器就不再自动创建默认构造方法

    // 有参构造函数
    public Student(String name, int age) {
        // 在方法内部，可以使用一个隐含的变量this，它始终指向当前实例
        // 没有命名冲突，可以省略this
        // 有局部变量和字段重名，那么局部变量优先级更高，就必须加上this
        this.name = name;
        this.age = age;
    }

    // 如果既要能使用带参数的构造方法，又想保留不带参数的构造方法，那么只能把两个构造方法都定义出来

    // 既对字段进行初始化，又在构造方法中对字段进行初始化,由于构造方方法后执行，所以字段值由构造方法执行结果决定

    // 可以有多个构造方法，方法名相同，参数不同，这称为方法重载
    // 调用另一个构造方法时，用this(...)调用
    public Student(String name) {
        this(name, 12); // 调用另一个构造方法Student(String, int)
    }

    // 方法
    public void study(String courseName) {
        System.out.println(this.name + "正在学习" + courseName);
    }
    // 定义方法
    修饰符 方法返回类型 方法名(方法参数列表) {
    若干方法语句;
    return 方法返回值;
}

}
// 创建实例
Student s = new Student();
s.name = "Xiao Ming"; // 为字段赋值
s.age = 12;
s.study("English"); // 调用方法

Student s2 = new Student();
s2.name = "Xiao Hong";
s2.age = 15;
s2.study("Art");
// s 和 s2 是两个不同的实例，它们各自拥有各自的字段和方法,且各自都有一份独立的数据，互不干扰.
```
### 2. 可变参数和参数绑定
- 可变参数
可变参数用类型...定义，可变参数相当于数组类型
> 可以把可变参数改写为String[]类型

> 可变参数可以保证无法传入null，因为传入0个参数时，接收到的实际值是一个空数组而不是null

```Java
class Group {
    private String[] names;
    // 可变参数names可以传入0个或任意个String
    public void setNames(String... names) {
        this.names = names;
    }
}

Group g = new Group();
g.setNames("Xiao Ming", "Xiao Hong", "Xiao Jun"); // 传入3个String
g.setNames("Xiao Ming", "Xiao Hong"); // 传入2个String
g.setNames("Xiao Ming"); // 传入1个String
g.setNames(); // 传入0个String

// 完全可以把可变参数改写为String[]类型
class Group {
    private String[] names;

    public void setNames(String[] names) {
        this.names = names;
    }
}
// 但是，调用方需要自己先构造String[]
Group g = new Group();
g.setNames(new String[] { "Xiao Ming", "Xiao Hong", "Xiao Jun" });
// 并且调用方可以传入null

// 而可变参数可以保证无法传入null，因为传入0个参数时，接收到的实际值是一个空数组而不是null
```
- 参数绑定
调用方把参数传递给实例方法时，调用时传递的值会按参数位置一一绑定
> 基本类型参数的传递，是调用方值的复制。双方各自的后续修改，互不影响。

> 引用类型参数的传递，调用方的变量，和接收方的参数变量，指向的是同一个对象。双方任意一方对这个对象的修改，都会影响对方（因为指向同一个对象）

    基本数据类型：传递值的副本，方法内修改不影响原始值。
    对象引用类型：传递引用的副本，可修改引用所指向对象的内容，但重新赋值引用不会影响原始引用。
    String 具有特殊情况，由于其不可变性，修改引用看起来像创建新对象而不是修改原对象。


```Java
public class Main {
    public static void main(String[] args) {
        // 创建 Person 对象
        Person p = new Person();
        // 创建字符串变量 bob 并赋值为 "Bob"
        String bob = "Bob";
        // 调用 Person 的 setName 方法，将 bob 所引用的 "Bob" 传递给 Person 的 name 属性
        p.setName(bob); 
        // 输出 Person 的 name 属性，此时为 "Bob"
        System.out.println(p.getName()); 
        // 改变 bob 变量的引用，使其指向新的字符串 "Alice"
        bob = "Alice"; 
        // 输出 Person 的 name 属性，仍然为 "Bob"
        System.out.println(p.getName()); 
    }
}

class Person {
    // 存储名字的私有属性
    private String name;

    // 获取 name 属性的方法
    public String getName() {
        return this.name;
    }

    // 设置 name 属性的方法
    public void setName(String name) {
        this.name = name;
    }
}
// name 指向 bob 所指向的对象（即 "Bob"），而不是指向 bob 变量本身
// 字符串的不变性是指引用永远指向同一个字符串，对字符串的修改实际上是创建了一个新的字符串对象，并且让引用指向这个新的字符串
```

```Java
public class Main {
    public static void main(String[] args) {
        // 创建 Person 对象
        Person p = new Person();
        // 创建一个包含两个元素的 String 数组
        String[] fullname = new String[] { "Homer", "Simpson" };
        // 调用 Person 的 setName 方法，将 fullname 数组传递给 Person 的 name 属性
        p.setName(fullname); 
        // 输出 Person 的 name 属性，此时为 "Homer Simpson"
        System.out.println(p.getName()); 
        // 修改 fullname 数组的第一个元素为 "Bart"
        fullname[0] = "Bart"; 
        // 输出 Person 的 name 属性，此时为 "Bart Simpson"
        System.out.println(p.getName()); 
    }
}

class Person {
    // 存储名字的私有数组属性
    private String[] name;

    // 获取 name 属性的方法，将数组元素拼接并返回
    public String getName() {
        return this.name[0] + " " + this.name[1];
    }

    // 设置 name 属性的方法，存储传入的数组
    public void setName(String[] name) {
        this.name = name;
    }
}

// Person 类中的 name 属性指向的是 fullname 数组本身，而不是复制了 fullname 数组的内容。
// 对 fullname 数组元素的修改会反映在 Person 类的 name 属性中，因为它们引用的是同一个数组对象
```
### 3. 访问权限修饰符
- private 修饰的成员，无论子类还是非子类，在任何包下都无法访问
- default（即不使用任何修饰符） 修饰的成员仅允许同包中的子类和非子类访问，不同包中的子类和非子类无法访问
- protected 修饰的成员，同包和不同包中的子类都可访问，同包的非子类可以访问，但不同包中的非子类不能访问
- public 修饰的成员，对于任何子类和非子类，在任何包下都能访问
### 4. 继承和多态
#### 继承
+ Java使用extends关键字来实现继承
+ 子类自动获得了父类的所有字段，严禁定义与父类重名的字段！
+ 一个类有且仅有一个父类。只有Object特殊，它没有父类, 它是所有类的父类。

继承的特点：
> 1. 子类无法访问父类的private字段或者private方法
> 2. 用protected修饰的字段可以被子类访问
> 3. 一个protected字段和方法可以被其子类，以及子类的子类所访问
> 4. 当子类继承时, 父类没有无参构造器时,需显式调用父类的构造器, 调用父类的构造方法必须放在子类构造方法的第一行
> 5. 当子类未重写继承的字段和方法时, 编译器会沿着继承链向上查找, 直到找到一个拥有该字段的类或到达Object类为止. 此时无论调用this.字段或直接调用字段,编译器都会自动定义到父类的字段
> 6. 使用super关键字调用父类的方法或字段
> 7. 子类不继承任何父类的构造方法
> 8. 用 final 修饰的类不能被继承

例子:
```Java
public class Demo {
    public static void main(String[] args) {
        Student s = new Student("小红", 12, 19);
        // 从内存角度看,当创建子类对象时,父类的字段和子类的字段都存储在子类对象的内存空间
        // 编译器根据对象的内存布局找到相应的存储位置进行访问
        // 由于子类没有重写name和age字段,所以将访问父类的字段
        System.out.println(s.name + " " + s.age + " " + s.getId()); // 小王 11 19
        s.get(); // 小王 11
    }
}
class Person {
    protected String name;
    protected int age;
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
// 使用 extends 关键字实现继承
class Student extends Person {
    private int id;
    public Student(String name, int age, int id) {

        // 编译器会自动调用父类的构造方法 super();
        // 调用父类的构造方法必须放在子类构造方法的第一行
        // 由于Person父类无无参构造方法，所以必须显式调用父类的构造方法
        super(name, age); // 显示调用父类的构造方法

        this.id = id;
        // 由于Student类继承了访问Person类成员的权利, 但Student类未拥有自己的name和age字段
        // 编译器会沿着继承链向上查找，直到找到一个拥有name和age字段的类或到达Object类为止
        // 此时无论调用this.name,name,编译器都会自动定义到父类的name和age字段
        this.name = "小王";
        this.age = 11;
    }
    public int getId() {
        return id;
    }
    public void get() {
        // 使用super关键字调用父类的方法或字段
        System.out.println(super.name + " " + super.age);
    }
}
```
// 上下对比思考
```Java
public class Demo {
    public static void main(String[] args) {
        Student s = new Student("小红", 12, 19);
        System.out.println(s.name + " " + s.age + " " + s.getId()); // 小王 11 19
        s.get(); // 小红 12
    }
}
class Person {
    protected String name;
    protected int age;
    public Person() {}
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

class Student extends Person {
    public String name;
    public int age;
    private int id;
    public Student(String name, int age, int id) {
        super(name, age); // 显式调用父类的构造方法
        // 由于父类有无参构造器,所以可以不用显式调用父类的构造方法,编译器会自动调用父类的无参构造方法
        // 当不显式调用时, s.get() 会输出 null 0
        this.id = id;
        // Student类拥有自己的name和age字段，所以this.name和this.age引用的是Student类的字段
        this.name = "小王";
        this.age = 11;
    }
    public int getId() {
        return id;
    }
    public void get() {
        System.out.println(super.name + " " + super.age);
    }
}
```

- 指定继承类
> final 表示该类不能再被继承，sealed 表示该类也可以限制它的子类，non-sealed 表示该类可以被任意类继承

```Java
// 指定继承类
// 用 sealed 修饰符定义一个受限制的类,该类只能被指定的子类继承, 需通过 permits 明确指出
sealed class Person permits Teacher, Student {
}
// 继承 sealed 类的子类必须使用 final、sealed 或 non-sealed 修饰符
final class Student extends Person {
}
// 用 sealed 修饰的被指定的子类需被final、sealed 或 non-sealed 修饰的类来继承
sealed class Teacher extends Person {
}

final class Teachers extends Teacher {
}
```
#### 向上转型和向下转型

> 向上转型 父类的引用变量可以指向子类的实例
> 向下转型 父类的引用变量可以强制转型为子类的实例

```Java
public class Demo {
    public static void main(String[] args) {
        // 类型为Person的引用变量p指向Person实例
        Person p = new Person();
        // 类型为Student的引用变量s指向Student实例
        Student s = new Student();

        // 向上转型 父类的引用变量可以指向子类的实例
        // 类型为Person的引用变量p2指向Student实例
        Person p2 = new Student();

        // 向下转型 父类的引用变量可以强制转型为子类的实例
        // s = p; 编译错误，无法将指向父类的实例的父类的引用变量强制转型为子类的实例
        if (p2 instanceof Student) {
            s = (Student)p2;
            System.out.println(s.Max_age);
        }
        // 从Java 14开始，判断instanceof后，可以直接转型为指定变量，避免再次强制转型
        if (p2 instanceof Student s2) {
            System.out.println(s2.Max_age);
        }
    }
}

class Person {
public int Max_age = 100;
}

class Student extends Person {

}
```

#### 多态
> 由于多态的存在，每个子类都可以覆写父类的方法
> Java的实例方法调用是基于运行时的实际类型的动态调用，而非变量的声明类型。
> 简而言之，看的是对象的实际指向类型。
> 要调用父类的被覆写的方法，可以通过super来调用
> 一个父类不允许子类对它的某个方法进行覆写，可以把该方法标记为final

```Java
public class Demo {
    public static void main(String[] args) {
        Person p = new Person();
        Person p2 = new Student();

        // Java的实例方法调用是基于运行时的实际类型的动态调用，而非变量的声明类型。
        p.run(); // Person 100
        p2.run(); // Student 100

        p2.getMax_age(); // Student person 100

        System.out.println(p.toString()); // [100]
    }
}

class Person {
    public int Max_age = 100;

    // 覆写Object方法
    @Override
    public String toString() {
        return "[" + Max_age + "]";
    }

    public void run() {
        System.out.println("Person" + " " + Max_age);
    }
    public void getMax_age() {
        System.out.println("person" + " " + Max_age);
    }
    // 用final修饰的方法不能被覆写
    public final void getDemo() {}
}

class Student extends Person {
    // 覆写Override
    // 方法签名相同,返回值相同
    @Override
    public void run() {
        System.out.println("Student" + " " + Max_age);
    }
    @Override
    public void getMax_age() {
        System.out.print("Student" + " ");
        // 子类中调用父类的被覆写的方法
        super.getMax_age();
    }
}
```
### 5. 抽象类和接口
#### 抽象类
> 如果父类的方法本身不需要实现任何功能，仅仅是为了定义方法签名，目的是让子类去覆写它，那么，可以把父类的方法声明为抽象方法
> 通过abstract定义的方法是抽象方法，它只有定义，没有实现。抽象方法定义了子类必须实现的接口规范
> 定义了抽象方法的class必须被定义为抽象类，从抽象类继承的子类必须实现抽象方法
> 如果不实现抽象方法，则该子类仍是一个抽象类
> 抽象类可以有字段
> 抽象类可以定义非抽象方法
```Java
public class Demo {
    public static void main(String[] args) {
        // 可以通过抽象类Person类型去引用具体的子类的实例
        Person p = new Student();
        Person p2 = new Teacher();

        p.run(); // Student run
        p2.run(); // Teacher run
    }
}

abstract class Person {
    public abstract void run();
}
class Student extends Person {
    @Override
    public void run() {
        System.out.println("Student" + " run");
    }
}
class Teacher extends Person {
    @Override
    public void run() {
        System.out.println("Teacher" + " run");
    }
}
// 如果不实现抽象方法，则该子类仍是一个抽象类
abstract class People extends Person {}
```
#### 接口
抽象类和接口的对比

| | abstract class | interface |
| :--: | :--: | :--: |
| 继承 | 只能extends一个class | 可以implements多个interface |
| 字段 | 可以定义实例字段 | 不能定义实例字段 |
| 抽象方法 | 可以定义抽象方法 |	可以定义抽象方法 |
| 非抽象方法 | 可以定义非抽象方法 | 可以定义default方法 |



> 接口interface没有实例字段, 但可以有静态字段, 并且静态字段必须为 final 类型
> 所有方法为抽象方法
> 接口定义的方法默认为 public abstract, 所以定义时这两个修饰符可以省略
> 接口定义的静态字段默认为 public static final 类型, 所有这些修饰符可以省略
> 一个类只能继承另一个类,但可以实现多个接口
> 接口可以继承接口
> 在接口中可以定义 default 方法
> 接口也是数据类型,适用于向上转型和向下转型

```Java
public class Demo {
    public static void main(String[] args) {
        People p = new Student("小红", 12);

        p.run(); // 小红 run
        p.getDemo(); // 小红 getDemo
    }
}
interface Person {
    void run();
    String getName();
}
interface People extends Person {
    int getAge();
    // 实现类可以不必覆写 default 方法
    // 相当于继承, 实现类可以调用, 在需要覆写时覆写
    default void getDemo() {
        System.out.println(getName() + " getDemo");
    }
}

class Student implements Person, People {
    private String name;
    private int age;
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public void run() {
        System.out.println(getName() + " run");
    }
    @Override
    public String getName() {
        return name;
    }
    @Override
    public int getAge() {
        return age;
    }
}
```
### 6. 静态字段和静态方法

> 推荐用类名来访问静态字段。可以把静态字段理解为描述class本身的字段
> 静态字段属于所有实例“共享”的字段，实际上是属于class的字段
> 调用静态方法不需要实例，无法访问this，但可以访问静态字段和其他静态方法
> interface是可以有静态字段的，并且静态字段必须为final类型
> 实例对象能访问静态字段只是因为编译器可以根据实例类型自动转换为类名.静态字段来访问静态对象

```Java
public class Demo {
    public static void main(String[] args) {
        Student.setAge(12);
        System.out.println(Student.age); // 12
        System.out.println(Student.Max_age); // 100
    }
}
interface Person {
    // 因为interface的字段只能是public static final类型，所以我们可以把这些修饰符都去掉
    // 简写为 int Max_age = 100;
    // 编译器会自动把该字段变为public static final类型
    public static final int Max_age = 100;
}
class Student implements Person {
    public static int age;
    public static void setAge(int number) {
        age = number;
    }
}
```
### 7. 包和作用域
#### 包
> 一个类总是属于某个包，真正的完整类名是包名.类名
> 在Java虚拟机执行的时候，JVM只看完整类名，因此，只要包名不同，类就不同。
> 包没有父子关系。java.util和java.util.zip是不同的包，两者没有任何继承关系。

- 位于同一个包的类，可以访问包作用域的字段和方法。不用public、protected、private修饰的字段和方法就是包作用域
```Java
// 位于hello包的Person类
package hello;

public class Person {
    // 包作用域:
    void hello() {
        System.out.println("Hello!");
    }
}
```
Main类也定义在hello包下面
```Java
package hello;

public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        p.hello(); // 可以调用，因为Main和Person在同一个包
    }
}
```
- import
> 不同包中调用,直接写出完整类名
> 用import语句导入不同包中的类
> 在写import的时候，可以使用*，表示把这个包下面的所有class都导入进来（但不包括子包的class）
> import static 语法, 导入一个类的静态字段和静态方法,可以直接调用静态字段或方法

位于demo_two.mr.jun包的Arrays类
```Java
package demo_two.mr.jun;

public class Arrays {
}
```
位于demo_two.hong包的Person类
```Java
package demo_two.hong;

public class Person {
    public static int num = 100;
    public int num2 = 200;
    public static void run() {
        System.out.println("hong static run");
    }
    public void run2() {
        System.out.println("hong run");
    }
}
```
位于demo_two.ming包的Person类
```Java
package demo_two.ming;
// 导入demo_two.mr.jun包中的Arrays类
import demo_two.mr.jun.Arrays;
// 静态导入demo_two.hong包中的静态字段和静态方法
import static demo_two.hong.Person.*;

public class Person {
    public static void main(String[] args) {
        // 不同包中调用
        // 1. 直接写出完整类名
        demo_two.mr.jun.Arrays arrays = new demo_two.mr.jun.Arrays();

        // 2. 用import语句导入不同包中的类
        // import demo_two.mr.jun.Arrays;
        // 在写import的时候，可以使用*，表示把这个包下面的所有class都导入进来（但不包括子包的class）
        // import demo_two.*; 导入demo_two包的所有class:
        // 导入后可以写简单类名
        Arrays arrays2 = new Arrays();

        // import static 语法, 导入一个类的静态字段和静态方法
        // 可以直接调用静态字段或方法
        System.out.println(num);
        run();
    }
}
```
### 8. 内部类和匿名类
#### 内部类
> Inner Class的实例不能单独存在，必须依附于一个Outer Class的实例
> 内部类可以直接访问Outer Class的private字段和方法
> 对于Inner Class和Outer Class的实例，只能访问自己的字段和方法
```Java
package demo;

public class Demo {
    public static void main(String[] args) {
        Person p = new Person(100);
        // 要实例化一个内部类Student，必须先实例化Person
        // 通过调用Person实例的new来创建内部类的实例
        Person.Student s = p.new Student();
        p.run1(); // Person run
        s.run2(); // Student run 100
        s.setAge(1000);
        s.run2(); // Student run 1000
    }
}
class Person {
    private int age;

    Person(int age) {
        this.age = age;
    }

    public void run1() {
        System.out.println("Person run");
    }

    class Student {
        private int age2 = 10;

        public void run2() {
            System.out.println("Student run " + Person.this.age);
        }

        public void setAge(int num) {
            age = num;
        }
    }
}
```
#### 匿名类
```Java
package demo;

public class Demo {
    public static void main(String[] args) {
        Outer o = new Outer("Outer");
        o.outerRun1(); // Outer Person run
        o.outerRun2(); // Outer People run
    }
}

interface Person {
    void run();
}

class People {
    public void run() {
        System.out.println("People run");
    }
}

class Outer {
    private String name;

    Outer(String name) {
        this.name = name;
    }

    void outerRun1() {
        // 匿名类实现接口
        Person p = new Person() {
            @Override
            public void run() {
                System.out.println(name + " Person run");
            }
        };
        p.run();
    }
    
    void outerRun2() {
        // 重写父类方法
        People p = new People() {
            @Override
            public void run() {
                System.out.println("Outer People run");
            }
        };
        p.run();
    }
}
```
#### 静态内部类
> static修饰的内部类和Inner Class有很大的不同，它不再依附于Outer的实例，而是一个完全独立的类
> 拥有Outer Class的private访问权限
```Java
package demo;

public class Demo {
    public static void main(String[] args) {
        // 静态内部类实例化
        // 不需要先实例化Outer，直接实例化静态内部类
        Outer.Inner i = new Outer.Inner();
        i.run(); // Inner Outer
    }
}
class Outer {
    private static String name = "Outer";

    static class Inner {
        void run() {
            System.out.println("Inner " + Outer.name);
        }
    }
}
```