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

- java 5 格式化输出 System.out.println()

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
    //使用带字符串
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
  -  mian 方法接收`String arg[]` 字符串数组 ，存储的是 命令行上指定的参数
- 数组排序
  - `Arrays.sort()` ：优化的快速排序算法
- 不规则数组
  -  Java 实际上没有多维数组，只有一维数组。多维数组被解释为 “数组的数组”

# 第四章 对象与类

