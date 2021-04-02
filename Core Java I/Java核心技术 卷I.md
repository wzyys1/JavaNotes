本书的示例源码网址: http://horstmann.com/corejava

# 第 三 章 Java 的基础设计结构

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
- **整型值和布尔值不能互相转换** :imp: :imp: :imp: 

## 3.4 常量与变量

- java10 开始 可以从变量初始值判断变量类型就不需要再声明类型，只需使用 `var` 关键字
- 常量关键字 `Final` , 使用 **全大写**。 类常量关键字 `static final`

## 3.5 运算符

- long Math.round()  四舍五入

## 3.6 字符串

- 子串 substring
- 静态join : 把多个字符串放在一起用 界定符 分隔
- repeat方法 重复
- 不可变字符串 **设计思想** : 共享所带来的高效率远远胜过他提取字符串、拼接字符串所带来的低效率
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

- java 5 格式化输出  `System.out.println()`

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

  - 必须是实现了  `Iterable`  的类
  - for 会遍历数据中的每一个 元素 而不是 下标
- 打印数组中元素的简单方法

  - `Arrays.toString(a)`  ,例如 `[2, 3, 5, 7, 11, 13]`
- 数组拷贝
  
  - 用同一个数组， 一个数组值变，另一个也变
- 将一个数组所有值拷贝到新的数组中 `Arrays.copyof(numbers, numbers.length * 2)`
- **命令行参数**
  - 每个 Java 程序 都会有一个带 `String arg[]` 的 main 方法，
  -  mian 方法接收 `String arg[]` 字符串数组 ，存储的是 命令行上指定的参数·
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

  **在一个源文件中，只能有一个公共类，但可以有任意数目的非公共类。源文件的文件名必须与 public 类的名字相匹配** ​ :imp: :imp: :imp: 

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

- Java 程序设计语言是**完全采用** `按值传递` 的  :imp: :imp: :imp:  

- 对象采用的不是`按引用传递`的，实际上，是对象引用 `按值传递`.(不要被对象状态改变的假象所迷惑， 是参数对象变量 对 堆中对象的状态的操作引起，对象引用是 按值传递 的)

 ## 4.6 对象构造

- 默认字段初始化

  - 如果没有显示的初始化字段，就会自动地赋为默认值

    | 数值 | 布尔值 | 对象引用 |
    | :--: | :----: | :------: |
    |  0   | false  |   null   |

- 对象的实例字段 默认值 不一定是 常数值 ，可以 是 赋予一个 方法调用

- `this`  另一个功能 : 调用另一个构造器

- 程序运行时：`静态初始化块` 最先被执行（只在程序第一次创建该类的对象时执行一次，创建包括第二个之后的对象就不会再执行），然后执行 `普通初始化块`（每次创建一个对象时都会执行）， 最后才执行 `构造方法 `。
  - `静态初试化块` 只在类加载的时候执行一次，同时 `静态初始化块` 只能给静态变量赋值，不能初始化普通的成员变量。 
  - `静态初始化块` 又叫 `类初始化块`， `普通初始化块` 又叫 `对象初始化块`

## 4.7 包

- 使用 `包` 的原因: 确保类名的唯一性
  - 为确保 类名 的绝对唯一性 ，包名 用一个 逆序形式的 `因特网域名`（这显然是唯一的）。
  - 从编译器的角度来看，**嵌套的包之间没有任何关系**，**每个包都是独立的类集合**。 eg： `java.util` 包 和  `java.util.jar` 包毫无关系。  :imp: :imp: :imp:  

- 一个类 可以使用所属包的 所有类， 以及其他包的                                                                                                                                                                            公共类
  - 使用 完全 限定名，包名 + 类名 eg ： `java.time.LocakDate today = java.time.LocakDate .now()`
  - 使用 `import` 导入，特定的类 或者 整个包
    - 允许 导入 `静态方法` 和 `静态字段` eg : ·`import static java.lang,System.*`  (不重要)
  
- 将 类 放入 `包` 中： 必须将 包的名字 放在源文件开头。如果 没有在 `源文件` 中放置 `package 语句`  这个源文件属于 `无名包`，无名包没有包名，编译器将 字节码文件 也放在相同 的目录结构中。

  ```java
  packge com.horstmann.corejava;
  public class Employee
  {
      ...
  }
  ```

- 如果 `包` 与 目录不匹配，虚拟机就找不到类。

- 访问权限  :imp:  :imp:  :imp:  

|      public      |       （default）        |        private         |
| :--------------: | :----------------------: | :--------------------: |
| 可以由任意类使用 | 被同一个包中所有方法访问 | 只能由定义他们的类使用 |

- `类路径 `：是所有包含类文件的路径的集合

  - 设置类路径，使 类 能被多个程序共享 至少应该包含：基目录、当前目录、JAR文件目录
    - 把类文件放在一个目录
    - JAR 文件 （ZIP 格式组织文件 和 子目录）放在一个目录
    - 类文件路径 ： .  : JAR 文件路径  

  - `类路径` 所列出的目录 和 归档文件（JAR） 是搜索类的 起点
  
- 虚拟机 先看 Java API类，找不到就 会 去 类路径找
  
- 设置 类路径： 
  
  - 用 `-classpath`  或者 `cp` 设置， 
  
      ```
      java -classpath  /home/user/classdir:.:/home/user/archives/archive.jar MyProg
      java -classparh c:\classdir:.:c:archives/archive.jar MyProg
    ```
  
  - 也可 通过 环境变量 `CLASSPATH` 来指定
  
      ```
      set CLASSPATH = c:\classdir:.:c:archives/archive.jar
    ```
  

## 4.8 JAR 文件

- Java归档（JAR）文件：将应用程序打包，只向用户提供一个单独文件。
- JAR是压缩的，用的 ZIP压缩格式。

	```
	// jar cvf jarFileName file1 file2 ...
	jar cvf CalculatorClasses.jar *.class icon.gif
	```

-  `清单文件`： 每个JAR都有一个 ，描述归档文件的特殊属性，被命名为 `MANIFEST.MF` 在JAR文件 `META-INF`子目录中。

## 4.9 文档注释

- 文档注释 用到 JDK 的 `javadoc` 工具，可以把 源文件 生成一个 HTML 文档。eg：联机文档                                       
  - 每个`/**...*/ ` 文档注释包含 `标记` + `自由格式文本`
  - 标记有很多种
    - 类注释
    - 方法注释： `@param` 、`@return`、`@throw`
    - 字段注释 
    - 通用注释： `@author`、 `@version`、 `@see`、`@link`
    - 包注释：需要在每一个包目录中添加一个单独的文件

- 注释抽取

  ```
  // 一个包
  javadoc -d docDirectory nameOfPackage
  // 多个包
  javadoc -d docDirectory nameOfPackage1 nameOfPackage2
  // 无名包
  javadoc -d docDirectory *.java
  ```

## 4.10 类设计技巧  

- 一定保证数据私有
- 一定要对数据进行初始化
- 不要在类中使用过多的基本类型
- 不是所有字段都需要单独的 字段访问器 和 字段更改器
- 分解有过多职责的类
- 类名与方法名能够体现他们的职责：有一个能反映其含义的名字
- 优化使用不可变的类



# 第五章 继承

## 5.1 类、超类和子类

- `extends` 表示 继承，java 中的 所有继承都是 `公有继承 `  (没有 c++ 中的 私有 和 保护继承) :imp: :imp: :imp: 

- 子类 调用 父类方法名时 用  `super. 超类方法名`

- `子类` 没有 显式 调用 `超类` 的 构造器，自动调用 `超类` 的 无参构造器，如果 `超类` 没有，`子类 ` 也没调用其他构造器，就会报错。:imp::imp::imp:

- 关键字 `this`
  - 指示隐式参数的 **引用**
  - 调用该类的其他构造器
  
- 关键词 `super` (**super 不是一个对象引用， 他只是一个 指示 编译器 调用 超类 方法的特殊关键字**）
  - 调用超类的方法
  - 调用超类的构造器
  
- Java 不支持 `多重继承`（即一个类 有多个超类）

- `对象变量` 是  `多态`  的。（理解运行时动态绑定的概念）:imp::imp::imp:
  
  - **如果 父类 引用了 子类对象，编译器 只是将 它看作为 父类对象。调用子类方法就可能会报错（如果子类定义，父类没有定义）。**
  
- **重载方法 在运行时 动态绑定，虚拟机会调用 所引用对象的实际类型对应的那个方法。（说的天花乱坠，其实就是 “运行时的多态”）**
  
  ---
  
  > `多态` 总结 :
  
  > - `重载解析`（词如其名，重载过程解析...）
  >   - 编译器确定方法调用中提供的参数类型，并去相同名字中去找与所提供的参数类型完全匹配的方法，如果存在，就选择这个方法
  >   - `方法的签名` : 方法名称 + 参数 （不包括方法返回值）
  > - `动态绑定` 与 `静态绑定` 
  >   - `静态绑定`  ： 编译器 准确知道调用哪个方法, private 方法、 static方法、 final方法、构造器
  >   - `动态绑定`： 要调用方法 依赖于 **隐式参数** 的 **实际**类型，必须在运行时使用动态绑定 ，采用该方法时，虚拟机必须调用与 该对象变量所引用 对象的实际类型对应的那个方法。（有调用，没有向上找，由于时间开销大，虚拟机预先会为每个类创建  `方法表 `  方便搜索）
  >   - java中 `动态绑定` 是 **默认的** , c++ 则需要将成员函数声明为 `virtual`， 如果不希望这样，在 java 中使用  `final`  修饰该函数）:imp::imp::imp:
  > - 多态其实就说了两个问题：
  >
  > 	1. 子类对象可以传给父类引用，但是只能调用父类的方法（如果调用实际类型的方法父类中没有定义会报错）
  > 	2. 如果子类把父类定义的方法覆盖了，虚拟机就会动态绑定，调用子类对应同名方法
  >
  
  ---
  
- 在覆盖一个方法的时候，子类方法 **不能低于** 超类方法的可见性。

- `final类` 会阻止继承 ，其中的所有方法都会 自动的 成为 final 方法，**而不包括 字段。**eg: String类 就是 final类

- `内联` ： 如果一个方法没有被覆盖并且很短，编译器就能够对他进行优化处理，这个过程称作：`内联` 。 eg：内联调用 e.getName() 将被替换为访问字段 e.name 

- 进行 `强制类型转换 ` 的唯一原因： 要在暂时忽视对象的 实际类型之后，使用对象的全部功能。
  - 只能在 继承层次（一个 公共超类 派生出来的所有类的 集合） 内进行 `强制类型转换`
    - 在将 `超类` 强制转换成 `子类` 之前，应该使用 `instanceof` 进行检查

- 包含一个或多个方法 必须声明为 `抽象类`，抽象类可以包含 字段 和 具体方法。扩展的抽象类还可以定义为`抽象类`，抽象类不能实例化。（对我来说，这个知识点其实不需要写，我早就记住了，略略略）

- 访问权限  :imp:  :imp:  :imp:  

|      public      | （default）  |           protected            |        private         |
| :--------------: | :----------: | :----------------------------: | :--------------------: |
| 可以由任意类使用 | 仅对本包可见 | 对本包 和 其他包的所有子类可见 | 只能由定义他们的类使用 |

## 5.2 Object：所有类的超类

- 在 Java 中，只有 基本类型 不是对象，所有数组类型（不管是 对象数组 还是 基本类型数组 ）都扩展了Object 类

  ```
  Employee[] staff = new Employee[10];
  obj = staff; // ok
  obj = new int[10]; // ok
  ```

- `equal方法`： 确定两个对象引用是否相等（还有基于状态检测是否相等）， 为了防止调用方法的对象为 null，可以采用 `Objects.equals()`  方法。

  - 子类可以有自己 相等性 概念，则 对称性需求 将强制使用 getClass 检测

  - 如果由超类决定 相等性 概念， 可以使用  `instanceof` 检测，这样可以在不同子类之间进行相等性比较

    ---

    > 完美  `equals `  方法建议：
    
    > - 显示参数命名为 `otherObject` 
    > - 检测 `this` 和  `otherObject` 是否相等
  	>	```java
			if(this == otherObect) return true;
				```
    > - 检测 `otherObject` 是否为 null，如果为 null，返回 false。
    > 	```java
    	if(otherObject == null) return false;
    > 	```
    > - 比较 `this`  与 `otherObject` 类  
    >	```java
      // 如果 equals 的语义可以在子类中改变，就使用 getClass检测：
    	if(getClass() != otherObject.getClass()) return false
	  	// 如果所有子类都有相同的 相等性 语义，可以在父类中 使用 instanceof 检测
  			if(!(otherObject instanceof ClassName) return false // ClassName子类变量名
  	>	```
    > - 将 `otherObject ` 强制转换为相应类类型变量
    >	```java
    	ClassName other = （ClassName）otherObject
    >	```
    > - 根据相等的概念来比较字段，使用 `==` 来比较 基本类型字段，使用  `Objects.equals`  比较对象字段。 
    > 	```java
    	return field1 == other.field1
    			&& Objects.equals(field2, other.field2)
    			&& ...;
    >	```
  	> - 在子类重新定义了 `equals`,就要在其中包含一个 `super.equals(other)` 调用
  	
  	---
  
- `getClass方法 ` : 返回这个对象运行时的类( 返回Class类型的对象 )

- 如果要定义一个 覆盖超类方法的 子类方法，可以使用 `Override 标记` 。如果这个方法并没有覆盖超类的任何方法，就会看到一个错误报告。

- `散列码`（hash code）: 由对象导出的一个 **整型** 值 。

  - `Object类` 的 hashcode 由 **对象的存储地址** 导出
  - String 的散列码 hashcode 的由 **内容** 导出（这就是为什么一样内容的 String 字符串导出的 hashcode值相同）

  	```java
  	// Sting 类型中的 hashcode 定义方式
  	int hash = 0
  	for(int i = 0; i.length(); i++)
      	hash = 31 * hash + charAt(i);
  	```

  - 重新定义了 `equals方法`，就要重新定义 `hashcode方法`, 两者必须 **相容**（`equal方法` 返回 true， `hashcode方法` 必须返回相同的值 ） eg：如果比较 Employee.equals 比较员工 ID， 则 `hashcode方法` 就需要散列 ID，而不是 姓名 和 存储地址
  - 合理组合实例字段散列码，以便能让不同对象产生的散列码分布更均匀 
    - 可用 `objects.hash(args1,...,argsn)` ：对各个参数调用`Objects.hashCode()`,并组合这些散列码
    - 数组可用 `Arrays.hashCode(xxx[] a)` , 散列码由数组元素的散列码组成

- `toString方法` ：返回表示对象值的一个字符串。

  - 遵循格式一般为：类名 （`getClass().getName`）+  一对方括号括起来的字段值。
  - 只要对象与  `+` 号连接起来。Java编译器就会自动调用 `toString 方法` 来 获取这个 对象的字符串描述

  - `Object类` 定义的 `toString方法` 。可以打印对象的 类名 和 散列码
  - 数组继承了`Object类` 的 `toString方法` ，想要格式打印使用：`Arrays.toString`


## 5.3 泛型数组列表 - ArrayList

- 在老版本中，使用 `vector类` 实现动态数组，但目前 `ArrayList类` 更加高效，因舍弃以前的

- 如果估计出数组可能存储的 元素数量， 可以调用 `ensureCapacity` 方法，这样前 n 次add调用不会带来开销很大的重新分配空间。

- `trimToSize方法`： 将存储块大小调整为保存当前元素数量所需要的 存储空间，垃圾回收器将回收多余空间

- 自动扩容的便利，增加了访问元素语法的复杂程度。必须使用 `get` 和 `set` 方法。

- `ArrayList` 需要掌握的方法:
  - `E set(int index, E obj)` 
  - `E get(int index)`
  - `void add(int index, E obj)` 
  - `E remove(int index)`

	---
	> 小技巧  : 既可以灵活扩展数组，又可以方便访问数组元素

	>	```java
	>	var list = new ArrayList<X>();
	>	while(...){
	>		x = ...;
	>		list.add(x);
	>	}
	>	
	>	var a = new X[list.size()]
	>	list.toArray(a)
	>```
	
	---

## 5.4 对象包装器 与 自动装箱

- `包装器类` 是 **不可变** 的， 一旦构造，不允许更改包装在其中的值。包装器是 `final`，不能派生他的子类
- 自动装箱 和拆箱 是 `编译器` 的工作，不是 `虚拟机` 的。`编译器` 在生成类的字节码时就会插入必要的 方法调用，`虚拟机` 只是执行 这些字节码

## 5.5 参数数量可变的方法

- 方法参数列表用到 `...`,  相当于一个对应数据类型的数组，举个例子，

  ```java
  // 与 double[] 完全一样
  public static double max(double... values)
  ```

## 5.6 枚举类

 