本书的示例源码网址: http://horstmann.com/corejava

# 第 3 章 Java 的基础设计结构

## 3. 1 有个简单java应用程序 

1. Java区分大小写
2. 源代码文件必须和  `公共类名`  的名字相同
3. 回车不是结束符，如果需要可以将一条语句写到多行上

## 3.2 注释

1. //
2. /* */
3. /** */  可以用来自动生成文件

## 3.3  数据类型

- java 是 **强类型语言**
- int 返回 正负 刚刚超过 20亿
- **整型值和布尔值不能互相转换**

## 3.4 常量与变量

- java10 开始 可以从变量初始值判断变量类型就不需要再声明类型，只需使用 `var` 关键字
- 常量关键字 `Final` , 使用 全大写。 类常量关键字 `static final`

## 3.5 运算符

- long Math.round()  四舍五入

## 3.6 字符串

- 子串 substring
- 静态join : 把多个字符串放在一起用 界定符 分隔
- repeat方法 重复
- 不可变字符串设计思想 : 共享所带来的高效率远远胜过他提取字符串、拼接字符串所带来的低效率
- 检测两个字符串是否相等 equals() 如果不区分大小写：equalsIgnoreCase（）
- 码点与代码单元、
  - 码点：与一个编码表中的某个字符对应的代码值
  - 代码单元：在基本读语言平面中，每个字符用 16 位表示
- 联机 API 文档地址 : http://docs.oracle.com/javase/9/docs/api

- 如果是用较短的字符串构建字符串用 `StringBuilder`  构建，如果是更偏于共享就直接用`string`类

  - **StringBuilder**
    - append()
    - toString()

  - `StringBulider` 的前身 `StringBuffer` 效率低，但可采用多线程执行，如果在单线程执行用 StringBuilder

## 3.7 输入与输出

- java 6 读取控制台密码，用 console 类，为了安全，返回的密码存放在一个字符数组中。

- java 5 格式化输出 `System.out.println()`

	```java
Double x = 10000.0 / 3.0;
System.out.println("%8.2", x);
// 输出结果 3333.33
// 包含 8 个字符，精度为小数点后 2 个字符 这里打印一个 “前导空格” 和 7 个字符
	```

- 可以使用 String.format方法 创建一个格式化的字符串，而不打印输出

  ```java
  String message = String.format("Hello, %s. Next year,you'll be %d", name, age);
  ```

- 文件输入与输出

  - 读取文件

    ```java
    // Scanner(Path p, String encoding)
    // 构造一个使用给定字符编码 encoding， 从给定路径读取数据的 Scanner
    Scanner in = new Scanner(Path.of("myfile.txt"), StandardCharsets.UTF_8)
    ```
  
  - 写入文件
  
    ```java
    // PrintWriter(String fileName)
    PrintWriter out = new PrintWriter("myfile.txt", StandardCharsets.UTF_8)
    ```

## 3.8 控制流程

- 不能在嵌套的两个块中声明同名变量

- `带标签的break` ：用于跳出多重嵌套的循环语句

  - 只能跳出语句块，不能跳入

  - 标签必须放在希望跳出的最外层循环之前，并且必须紧跟一个冒号

## 3.9 大数

- 如果基本整数和浮点数精度不能满足需求，可以使用 `java.math ` 包下的两个类 ： 

  - `BigInteger`  实现任意精度的 整数运算

  - `BigDecimal` 实现任意精度的 浮点数运算

    ```java
    // 普通数值转换为大整数 
    BigInteger a = BigInteger.valueof(100);
    // 使用带字符串
    BigInteger reallyBig = new BigInteger("223234325373535353535");
    ```
  
  - 大数需要使用 add() 和multiply () 
  
    ```java
    lotteryOdds = lotteryOdds * (n - i + 1) / i;
    // 如果使用大数
    lotteryOdds = lotteryOdds.miltiply(BigInteger.valueOf(n - i + 1)).divide(BigInteger.valueOf(i));
    ```
  
    

## 3.10 数组

- 声明数组

  ```java
  int[] a;
  ```

- 声明并初始化

  ```java
  int[] a = new int[100];
  ```

- 创建对象并提供初始值

  ```java
  int[] smallPrimes = {2,3,5,7,11,13,};
  // 重新初始化
  smallPrimes = new int[]{17,19,23,31,37};
  ```

- 数组默认初始化

  |        | 数字数组 | boolean数组 | 对象数组 |
  | :----: | :------: | :---------: | :------: |
  | 初始值 |    0     |    false    |   null   |


- 增强 for 循环  `for each`

  - 依次处理数组中的每个元素，不用考虑下标

  - 必须是实现了  `Iterable` 的类
  - for 会遍历数据中的每一个 元素 而不是 下标
- 打印数组中元素的简单方法

  - `Arrays.toString(a)`  ,例如 `[2, 3, 5, 7, 11, 13]`
- 数组拷贝
  
  - 用同一个数组， 一个数组值变，另一个也变
- 将一个数组所有值拷贝到新的数组中 `Arrays.copyof(numbers, numbers.length * 2)`
- **命令行参数**
  - 每个 Java 程序 都会有一个带 `String arg[]` 的 main 方法，
  -  mian 方法接收`String arg[]` 字符串数组 ，存储的是 命令行上指定的参数·
- 数组排序
  - `Arrays.sort()` ：优化的快速排序算法
- 不规则数组
  -  Java 实际上没有多维数组，只有一维数组。多维数组被解释为 “数组的数组”



# 第四章 对象与类

## 4.1面向对象程序设计

- 封装（数据隐藏）：将 `数据` 和 `行为` 分装在一个包中，并对对象的使用者隐藏具体的实现方式。
  - 对象中的数据从称为 `实例字段`, 操作数据的过程称为方法

- 对象的主要特性
  - 行为、状态、标识
- 类之间的关系
  - 依赖（“users-a”）: 一个类的方法使用或操纵另一个类的对象，我们就说一个类依赖于另一个类，减少依赖，减少类之间的耦合
  - 聚合（“has -a”）: 包容关系意味着类A的对象包含类B的对象
  - 继承（“is-a”）: 表述一个更特殊的类和一个更一般的类之间的关系

## 4.2 使用预定义类

- 对象与对象变量

  对象变量并没有实际包含对象，他只是引用了一个对象

  ```java
  Date deadline // 对象变量
  deadline =  new Date() // 对象变量 “引用” 一个对象
  ```

- **所有Java对象都存储在堆中**：当一个对象包含另一个对象变量时，他只是包含着另一个堆对象的指针。

- 时间是用距离一个固定 时间点 的毫秒数表示，这个 时间点 就是所谓的`纪元`，

  - `UTC `（Coordinated Universal Time,  国际协调时间） 时间是：1970年 1 月 1 日 00：00：00
  - `GMT`（Greenwich Mean Time, 格林尼治时间）

- `LocalDate` 1.8

  ```java
  LocalDate.now() // 使用 静态工厂 方法帮你调用构造器
  LocalDate newYearEve = LocalDate.of(1999, 12, 31);
  LocalDate aThousandDaysLater = newYearEve.plusDays(1000);
  int year = aThousandDaysLater.getYear(); // 2002
  int month = aThousandDaysLater.getMonthValue(); // 09
  int day = aThousandDaysLater.getDayofMonth(); // 2002
  ```

- 访问器方法 与 更改器方法

  - 访问器方法: 只访问对象而不修改对象的方法

## 4.3 用户自定义类

- ***基础 重点***：

  **在一个源文件中，只能有一个公共类，但可以有任意数目的非公共类。源文件的文件名必须与 public 类的名字相匹配** ​ :imp:  :imp:  :imp: 

- 关于编译（不重要的知识）

  如果只编译带有 `main函数` 的类，如果在 `main函数` 中用到了 另一个类文件，就会去找 `.class` ,没有找到，就会自动搜索，编译对应的 `.java` 文件.如果已有 `.class` 被更新，就会重新编译该文件

- 实例字段

  - 关键字 `public` : 意味着 任何类 、任何方法都可以调用这些方法

  - 关键字 `private`： 只有类自身的方法能够访问这些实例字段， 其他类的方法不能够读写这些字段
- **Java 中的所有对象都是在堆中构造的**  :imp: :imp: :imp:  

- 用 `var`  声明 **局部变量**

  java10 开始，倘若无需了解任何 Java API 就能从等号右边明显 看出类型 ，在这种情况下都可以使用 `var` 表示

- `null` 引用 注意事项

  - 如果对 `null` 值应用一个方法，会产生 `NullPointerException` 异常
  - Java9 中, `Objects` 类提供了一个便捷的方法：
    - “宽容型 ”： `Objects.requireNonNullElse (T obj, T defaultObj) `  
    - “严格型”： `Objects.requireNonNull(T obj, String message)`

- 关键词 `this` 指示隐式参数，这样可以将 实例字段 与 局部变量 明显的分开

- 为防止 封装性被破坏，不要返回可变对象的引用。如果需要返回可变对象的引用，首先应该对他进行**克隆**。

- **一个方法** 可以访问 **所属类的所有对象** 的 私有数据

- `不可变类`： 如果类中的所有方法都不会改变其对象，这样的类就是不可变类。

## 4.4 静态字段 与 静态方法

- 静态字段

  -  `静态实例字段` : 属于类，也称 `类字段`,它属于类而不属于任何单个的对象

  - `静态常量` : 类名.静态常量名。 已经多次使用的静态常量 `System.out`

    ```java
    public class System
    {
        ...
        public static final PrintStream out = ...;
        ...
    }
    ```

- 静态方法，可以认为 静态方法 是没有隐式参数 （this参数的方法）

  - 类的静态方法 **不能** 访问实例字段，因为他不能在对象上执行操作（没隐式参数 this 指针）
  - 静态方法可以访问静态字段
  - 以下两种情况可以用静态方法
    - 方法不需要访问对象的状态，因为他需要的参数都通过显示提供
    - 方法只需要访问类的静态字段

  - main 也是静态方法， 每个类都可以有一个main方法，这是常用于对类进行 `单元测试` 的一个技巧。

    ```java
    public class StaticTest{
        public static void main(String[] args){
            ...
        }
    }
    
    class Employee{
        ...
        实例字段
        ...
        实例方法
        ...
        public static void main(String[] args){
            ...
        } 
    }
    
    // 用于 单元测试
    java Employee
    // 普通
    java StaticTest
    ```

## 4.5 方法参数

- Java 程序设计语言是**完全采用** `按值传递` 的  :imp:  :imp:  :imp:  

- 对象采用的不是`按引用传递`的，实际上，是对象引用 `按值传递`.(不要被对象状态改变的假象所迷惑， 是参数对象变量 对 堆中对象的状态的操作引起，对象引用是 按值传递 的)

 ## 4.6 对象构造

