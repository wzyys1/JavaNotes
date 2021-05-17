本书的示例源码网址: http://horstmann.com/corejava

# 第三章 Java的基础设计结构

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

- 子类 调用 父类方法时 用  `super. 超类方法名()`

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
  >   - `动态绑定`： 要调用方法 依赖于 **隐式参数** 的 **实际**类型，必须在运行时使用动态绑定 ，采用该方法时，虚拟机必须调用与 该对象变量所引用 对象的实际类型对应的那个方法。（有调用，没有向上找，由于时间开销大，虚拟机是预先会为每个类创建  `方法表 `  方便搜索）
  >   - java中 `动态绑定` 是 **默认的** , c++ 则需要将成员函数声明为 `virtual`， 如果不希望这样，在 java 中使用  `final`  修饰该函数）:imp::imp::imp:
  > - 多态其实就说了两个问题：:imp::imp::imp:
  >
  > 	1. 子类对象可以传给父类引用，但是只能调用父类的方法（如果调用实际类型的方法父类中没有定义会报错）
  > 	2. 如果子类把父类定义的方法覆盖了，虚拟机就会动态绑定，调用子类对应同名方法
  
  ---
  
- 在覆盖一个方法的时候，子类方法 **不能低于** 超类方法的可见性。

- `final类` 会阻止继承 ，其中的所有方法都会 自动的 成为 final 方法，**而不包括 字段。**eg: String类 就是 final类

- `内联` ： 如果一个方法没有被覆盖并且很短，编译器就能够对他进行优化处理，这个过程称作：`内联` 。 eg：内联调用 e.getName() 将被替换为访问字段 e.name 

- 进行 `强制类型转换 ` 的唯一原因： 要在暂时忽视对象的 实际类型之后，使用对象的全部功能。
  - 只能在 继承层次（一个 公共超类 派生出来的所有类的 集合） 内进行 `强制类型转换`
    - 在将 `超类` 强制转换成 `子类` 之前，应该使用 `instanceof` 进行检查

- ~~包含一个或多个方法 必须声明为 `抽象类`，抽象类可以包含 字段 和 具体方法。扩展的抽象类还可以定义为`抽象类`，抽象类不能实例化。（对我来说，这个知识点其实不需要写，我早就记住了，略略略）~~

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

    > 完美  `equals `  方法建议： :imp:  :imp:  :imp:  
    
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

- 如果要定义一个 覆盖超类方法的 子类方法，可以使用 `Override标记` 。如果这个方法并没有覆盖超类的任何方法，就会看到一个错误报告。

- `散列码`（hash code）: 由对象导出的一个 **整型** 值 。 :imp:  :imp:  :imp:  

  - `Object类` 的 hashcode 由 **对象的存储地址** 导出
  - String 的散列码 hashcode 的由 **内容** 导出（这就是为什么一样内容的 String字符串 导出的 hashcode值相同） :imp:  :imp:  :imp:  

  	```java
  	// Sting类型 中的 hashcode 定义方式
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
  - 只要对象与  `+` 号连接起来。Java编译器就会自动调用 `toString 方法` 来 获取这个对象的字符串描述

  - `Object类` 定义的 `toString方法` 。可以打印对象的 类名 和 散列码
  - 数组继承了`Object类` 的 `toString方法` ，想要格式打印使用：`Arrays.toString()`


## 5.3 泛型数组列表 - ArrayList

- 在老版本中，使用 `vector类` 实现动态数组，但目前 `ArrayList类` 更加高效，因舍弃以前的。

- 如果估计出数组可能存储的 元素数量， 可以调用 `ensureCapacity` 方法，这样前 n 次add调用不会带来开销很大的重新分配空间。

- `trimToSize方法`： 将存储块大小调整为保存当前元素数量所需要的 存储空间，垃圾回收器将回收多余空间

- 自动扩容的便利，增加了访问元素语法的复杂程度。必须使用 `get` 和 `set` 方法访问和设置元素。

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
- 自动装箱 和拆箱 是 `编译器` 的工作，不是 `虚拟机` 的。`编译器` 在生成类的字节码时就会插入必要的方法调用，`虚拟机` 只是执行 这些字节码

## 5.5 参数数量可变的方法

- 方法参数列表用到 `...`,  相当于一个对应数据类型的数组，举个例子，

  ```java
  // 与 double[] 完全一样
  public static double max(double... values)
  ```

## 5.6 枚举类

- 自定义 `枚举类型`，`枚举类型` 包括有限个命名的值。

  ```java
  enum Size {SMALL, MEDIUM, LARGE, EXTRA_LARGE}
  // 声明 这种类型的变量
  Size s = Size.MEDIUM
  // Size类型 只能存储 这个类型声明中给定的某个枚举值， 或者 null
  ```

- 实际上声明定义的类型 是 **一个类**， 他刚好有 4 个对象（枚举**常量**） ，**不能再构造新的对象**。因此比较两个枚举类型值 时 用 `==` 而非 `equals` :imp:  :imp:  :imp:  

- 所有的枚举类型 都是 `Enum类` 的子类，继承了这个类很多方法

  - `toString()`， 返回枚举常量名  eg:  `Size.SMALL.toString() ` 返回字符串 “SMALL”

  - `valueOf()`, ` toString()` 逆方法,  返回给定类中有指定名字的枚举常量  (枚举对象)

    ```java
    // 将 是设置为 Size.SMALL
    Size s = Enum.valueOf(Size.class(), "SMALL")
    ```
    
  - `static values()`, 返回一个包含全部枚举值的数组 eg：`Size[] values = Size.values();`

  - `ordinal()`： 返回 enum 声明中 枚举常量的位置，从 0 开始计数 eg: `Suze.MEDIUM.ordinal()` 返回 1
## 5.7 反射

- `反射` ： 能够分析 类能力 的程序

- 程序运行期间，`Java运行时系统` 会始终为 所有对象 维护一个 `运行时类型标识`， 虚拟机利用这个信息选择要执行的正确的方法。他会跟踪每个对象所属类。可以使用一个特殊类访问这些信息，即 `Class类`。 

  - 就像之前 Employee对象 描述一个特定员工的属性一样，`Class对象` 会描述一个特定类的属性。

  - 获取 `Class对象` 的方法：

    - 使用 `Object类` 中的 `getClass方法`

      ```java
      Employee e;
      ... 
      Class cl = e.getClass();
      ```

    - 使用 `Class类` 的静态方法 `forName` 获得类名所对应的对象(字符串会变化，使用这个类)

      ```java
      String className = "java.util.Random";
      Class cl = Class.forName(className);
      ```

    - 如果 `T` 是 java 任意类型，使用 `T.class` 将代表匹配的 类对象。

      ```java
      Class cl1 = Random.class;
      Class cl2 = int.class;
      Class cl3 = DOuble[].class;
      ```

  - 一个 `Class对象` 实际上 **表示的是一个类型，**这可能是 一个类，也可能不是 ，eg： `int.class`

  - `Class类` 实际上是一个 泛型类。 eg： `Employee.class` 的类型是 `Class<Employee>`
  
  - 虚拟机为  **每个类型** 管理 **唯一 一个** `Class对象`。所以上一节中使用 `==` 实现两个类的比较（**言外之意是：判断是否属于同一个类生成的对象**）： `if(e.getClass() == Employee.class)` :imp:  :imp:  :imp:  
  
- 使用 `Class类` 对象，构造类的实例。调用 `getConstructor`  方法将得到一个`Constructor` 类型对象，然后使用`newInstance` 方法来构造实例

  ```java
  var className = "java.util.Random";
  Class cl = Class.forName(className);
  Object = cl.getConstructor().newInstance();
  ```

- `异常` 的种类：`非检查型异常` 和 `检查型异常`

  - `非检查型异常`：编译器不希望你对这些异常提供处理器。
  - `检查型异常`：编译器将会检查你（程序员）是否知道这个异常并做好准备来处理后果

- 利用反射分析类的能力：反射机制的重要内容 - `检查类结构`

  - `java.lang.reflect` 包中有三个类： `Field`、`Method`、`Constructor ` 分别用于描述类的字段、方法、和构造器。带 Declared 修饰的方法包括从超类继承过来的，不带的只是这个类的。
    - `Field[] getFields()`
    - `Field[] getDeclaredFields()`
    - `Method[] getMethods()`
    - `Method[] getDeclaredMethods()`
    - `Constructor[] getConstructors()`
    - `Constructor[] getDeclaredConstructors()`
  - 打印对应方法、字段、构造器的修饰符，先获取 修饰符 对应的整数值:  `cl.getModifiers()` , 然后利用该类的静态方法打印：`Modifier.toStirng(cl.getModifiers())`

- 使用 反射 在运行时分析对象: 可以利用反射机制, 查看在编译时还不知道的对象字段

  - `Field类` 的 `get方法` 可以获取对象字段的值，也可以通过 `set(obj,value)`设置对象字段的值

    - 下面例子有一处不恰当之处，`name` 是私有属性,会抛出 `IllegalAccessException异常` 。`Java安全机制` **允许查看有哪些字段，如果想读写哪些字段，除非拥有访问权限** 。:imp:  :imp:  :imp:  

    	```java
    	var harry = new Emptyee("Harry Hacker", 50000, 10, 1, 1989);
    	Class cl = harry.getClass();
    	Field f = cl.getDeclaredField("name");
    	Object v = f.get(harry)
    	```

  - `反射机制` 的 默认行为，受限制于Java的 `访问控制` 。可以用  `Field`、`Method`、`Constructor ` 的`setAccessible方法` 修改权限，但是也可能被拒绝。eg：`f.setAccessible(true);`

- 使用 `反射` 编写 通用 `泛型数组` 代码

  - 使用反射的 **核心原因**：可以 将得到的 `Object泛型数组` 转换回对应类型 。

  - `java.lang.reflect包` 中的 `Array类`，允许动态地创建数组

  	- 举一个 下面例子, 编写一个 通用方法
  
    	```java
    	var a = new Employee[100];
    	...
    	// 数组已满，需要扩充数组
  	a = Arrays.copyof(a, 2 * a.length);
    	```
  
    - 坏的尝试，由于java数组会记住每个元素的类型，即创建数组时候 new表达式 使用的类型。
    
      ```java
      public static Object[] badCopyOf(Object[] a, int newLength)
      {
      	var = newArray = new Object[newLength];
      	System.arraycopy(a, 0, newArray, 0, Math.min(a.length, newLength));
      	return newArray;
      }
      ```
    
    - 上面的不好的原因是：返回的 `Object[]数组` 无法转换成 `Employee[] 数组` 。因此，为了 **编写通用代码**，**需要能够创建与原数组类型相同的数组**。
    
      ```java
      Public static Object goodCopyof(Object a, int newLength)
      {
          // 获得 a 数组的类对象
          Class cl = a.getClass();
          // 确认他是一个数组
          if(!cl.isArray()) return null;
          // 确定数组的正确类型
          Class componentType = cl.getComponentType();
          int length = Array.getLength(a);
          Object newArray = Array.newInstance(componentType, newLength);
          System.arraycopy(a, 0, newArray, 0, Math.min(a.length, newLength));
      	return newArray;    
      }
      ```
    
      - 这里 用 `Object` 而不用 `Object[]` 的原因是：为了使该方法可以扩展 任意类型数组 而不单单是对象数组。
    
        ```java
        int[] a ={1, 2, 3, 4, 5};
        a = (int[]) goodCopyof(a.10);
        ```
  
- 可以利用 `反射机制` 调用 `任意的方法` 和 `构造器`
  
  - d调用`任意方法`： 1.获得  `Method 对象 ` 2. 调用 `invoke方法`
    
  - 例如 ： 可以利用 `Method类` 中的 `invoke方法` ，调用包装在当前 Method对象 中的方法
  
    ```java
    // Object invoke(Object obj, Object...args) 
    // 第一个 参数 是隐式参数（static 为 null）， 其余对象提供显式参数
    String n = (String) m1.invoke(harry)
    ```
  
  - 如何得到 `Method对象` 方法, 有下面两种。不过有若干种 **同名方法**，所以还必须提供方法的参数类型
  
    - 调用 `getDeclaredMethods方法`
  
    - 调用 `Class类` 的 `getMethod`       `
  
      ```java
      // Method getMethod(String name, Class... parameterTypes)
      // 说明了如何获得方法指针
      Method m1 = Employee.class.getMethod("getname");
      Method m2 = Employee.class.getMethod("raiseSalary", double.class);
      ```
  
  - 调用 `构造器` : 1. 获取  `Constructor对象` 2. 调用方法 `newInstance方法`
  
    - 将 参数类型 提供给  `Class.getConstructor方法` 
  
    - 把 参数值 提供给  `Constructor.newInstance方法`
  
      ```java
      Class cl = Random.class;
      Constructor cons = cl.getConstructor(long.class);
      Object obj = cons.newInstance(42L);
      ```
  
  - **使用反射获得的方法指针比直接调用慢很多**（因为来回强制类型转换需要花费大量时间）
  
- 反射总结：

  - 什么是 Class类
  - 分析 类的结构： 字段、方法、构造器
  - 在运行时 分析对象：主要是对象的字段
  - 写泛型数组代码
  - 调用 任意方法 和 构造器 ：方法指针

## 5.8 继承的设计技巧

- 将公共操作和字段放在超类中
- 不要使用受保护字段
- 使用 继承实现“is- a” 关系时，避免滥用
- 除非所有继承方法都有意义，否则不要使用继承
- 在覆盖方法时，不要改变预期行为
- 使用多态，而不要使用类型信息
- 不要滥用反射

# 第六章 接口、lambda表达式与内部类

## 6.1 接口

- `接口` : 他不是类，是对希望符合这个接口的类的一组需求

- `接口 ` 中 **所有方法** 都自动是 `public方法`。因此，在接口中声明方法时，不必提供关键字 `public`

- `接口` 可以定义 常量， 但是 **绝不会有** **实例字段**。:imp:  :imp:  :imp:  

  - 可以将接口其看成没有实例字段的抽象类。但两者还有着一定的区别，如果将接口设计为抽象类，会存在一个严重的问题，即：**每个类只能扩展一个类**，假设某个类已经扩展了别的类，他就不能再扩展第二个类了。（**Java不支持多重继承**）

- 一个具体例子：`Arrays类` 中 的 `sort()` 方法承诺可以对对象数组进行排序，但必须满足的条件是：对象所属类必须实现 `Comparable接口`

  ```java
  public interface Comparable
  {
  	int compareTo(Object other);
  }
  // java 5 开始
  public interface Comparable<T>
  {
  	int compareTo(T other);
  }
  ```

  - 假设希望使用 `Arrays类` 的 `sort方法` 对 `Employee对象数组` 进行排序, `Employee类` 就必须实现 `Comparable接口`

    ```java
    // 将类声明为实现给定接口
    class Employee implements Comparable
    {
        ......
        // 对接口中的所有方法提供定义
        public int compareTo(Object otherObject)
        {
        	Employee other = (Employee) otherObject;
            return Double.compare(salary, other.salary);
        }
    }
    // java 5 开始
    class Employee implements Comparable<Employee>
    {
        ......
        public int compareTo(Employee other)
        {
            return Double.compare(salary, other.salary);
        }
  }
    ```

  - `x.compareTo(y) ` : x 小于 y，返回负数；x 等于 y，返回0； x 大于 y，返回正数。

  - `Comparable接口  ` 的文档建议：`compareTo方法` 应当与 `equals方法` 兼容，也即是说当 `x.equals(y)` 时， `x.compareTo(y)` 就应该等于 0。

  - 如果比较的两个对象 一个是父类 eg：Employee，一个是子类 eg： Manager，`x.compareTo(y) ` 不会异常， `y.compareTo(x) ` 会出现异常 `ClassCastException`。（与 `equals方法` 相似）两种解决方法:imp:  :imp:  :imp:  

    - 不同子类中比较的含义不同时，就应该将属于不同类的对象之间的比较视为违法，在开始 `compareTo方法  ` 时，进行如下检查： `if(getClass() != other.getClass()) throw new ClassCastException()`

    - 如果存在一个比较子类对象的通用方法，那么可以在超类中提供一个 `compareTo方法  ` ，并将这个方法声明为 `final`
  
- ~~接口不是 类，不能用 new 运算符实例化一个接口，虽然不能构造接口对象 ，但是可以声明接口的引用变量。每个类只能有一个超类，但是可以**实现**多个接口~~

- 如同使用 `instanceof` 检查一个对象是否属于某个特定类一样，也可以使用 `instanceof` 检查一个对象是否实现了某个特定的接口:  `if(anObject instanceof Comparable){...}`

- 接口中的方法 都会被自动设置为 `public` ,接口中的字段总是 `public static final `:imp:  :imp:  :imp:  

- 以前的做法通常都是将 **静态方法** 放在 `伴随类` 中，在标准库中，你会看到成对出现的 `接口` 和 `实用工具类`，eg：`Collection/Collections` 或者 `Path/Paths` 。但是，在 `java8` 开始，**允许在接口中 增加 静态方法**，实现你的接口时，没有必要为实用工具方法另外提供 `伴随类`

- `java9` 中接口的方法可以是 `private`。`private方法` 可以是 `静态方法` 或 `实例方法`。他的用法很有限，只能作为接口中其他方法的辅助方法

- 可以为 接口 提供一个 默认实现（**默认方法**)，**必须**用 `default` 修饰符标记这样一个方法。默认方法的一个重要用法是 “**接口演化**”

  - 冲突问题：在一个接口将一个方法定义为默认方法，又在  超类 或 另外一个接口 中定义同样的方法，会发生 “**二义性**” 问题，解决规则如下：

    - `超类优先`： 如果超类提供一个具体方法，同名而且有相同类型参数的默认方法会被忽略
    - `接口冲突`： 如果一个接口提供一个默认方法，因一个接口提供了一个同名且参数类型相同（不论是否为默认方法）的方法，必须覆盖这个方法来解决冲突
    - 如果两个接口都没有给共享方法提供默认实现，这里就不存在冲突


- `回调` ： 是一种常见的程序设计模式。在这种模式中，可以指定某个特定事件发生时应该采取的动作。

- `Sting.compar()方法` 可以按照字典顺序比较字符串，可是当我们需要按照长度去比较字符串时，就需要实现 `Arrays.sort()` 的第二个版本：

  ```java
  public interface Comparator<T>{
      int comapre(T first, T second);
  }
  ```

  ​    按照长度实现可以定义下面这个类

  ```java
  class LengthComparator implements Comparator<String>
  {
  	public int compare(String first, String second)
  	{
  		return first.length() - second.length();
  	}
  }
  // 具体完成比较时，需要建立一个实例
  var comp = new LengthComparator()
  // 这个比较方法要在比较器对象上调用，而不是在字符串本身上调用
  if(comp.compare(words[i], words[j]) > 0) ...
  ```

  ​	对数组排序时，需要为 `Arrays.sort() `传入一个 `LengthComparator对象`

  ```java
  String friends = {"Peter", "Paul","Mary"};
  Arrays.sort(friends, new LengthComparator());
  ```

- `Cloneable` 接口:


  - `object类` 的 `clone`，他对这个对象一无所知, 所以这能逐个字段进行拷贝。如果是基本类型就没有问题，但是如果这个对象字段中包含对象引用（子对象是不可变不影响），这样一来拷贝下来仍然会出现局部共享。所以出现下面这两个概念：

    - `“浅拷贝”`: (Object类中clone方法的默认操作)：并没有clone 对象中字段引用的其他对象
    - `“深拷贝”`: 同时克隆所有子对象 
    
    - 对于每一个类需要确定：
      - 默认的 Object类 中的clone方法是否满足需求；
      - 是否可以在可变的子对象上调用 clone方法 来弥补默认的clone 方法，如果需要：
    
        - 实现 `Cloneable` 接口
        - 重新定义 clone 方法，并指定 `public` 访问修饰符

- `Object类` 中的 `clone方法` 声明为 `protected`, 所以不能在自己写的代码里调用 `anObject.clone`， 因为你的类不是 该对象的子类，且你可能和定义clone方法的类不在一个包下，所以在重新定义clone方法时，要指定为 public，以便所有方法都可以克隆对象

- `Cloneable接口` 没有 `clone方法` ，这个方法是从 `Object类` 继承的。它是Java中少数的 **标记接口** ，**标记接口** 不含任何方法，就是在类检查中允许使用 `instanceof`

- 即使默认 `clone方法`  实现能够满足要求，但还是需要实现 `Cloneable接口` , 将 clone 重新定义为 `public`, 在调用`super.clone()`。

    ```java
    class Employee implements Cloneable
    {
        // public access, change return type
        public Employee clone() throws CloneNotSupportedException
        {
            return (Employee)super.clone();
        }
        ...
    }
    ```

- “深拷贝” 需要克隆对象中可变的实例字段

    ```java
    class Employee implements Cloneable
    {
        ...
        // 在一个对象上调用 clone 方法，若没有实现Cloneable接口， 会抛出 
        //CloneNotSupportedException异常
        public Employee clone() throws CloneNotSupportedException
        {
            // call Object.clone()
            Employee cloned = (Employee) super.clone();
            
            // clone mutable fields
            cloned.hireDay = (Date) hireDay.clone();
            
            return cloned;
        }
    }
    ```

- 所有的数组类型都有一个 **公共的 ** `clone方法`，而不是 **受保护的**。可以用这个方法 建立一个新数组，包含原数组的所有副本。

  ```java
  int[] luckNumbers = {2, 3, 5, 7, 11, 13};
  int[] cloned = luckNumbers.clone();
  cloned[5] = 12 // doesn't change luckNumbers[5]
  ```

## 6.2 lambda 表达式

- `lambda表达式` ：是一个 `可传递的代码块`

  - 例子

    ```java
    class LengthComparator implements Comparator<String>
    {
    	public int compare(String first, String second)
    	{
    		return first.length() - second.length();
    	}
    }
    ...
    Arrays.sort(friends, new LengthComparator());
    ```

  - 这个例子的特点：将一个 **代码块** 传递给某个对象。这个代码块会在将来某个时间调用

  - 再出现这个与法之前，Java传递一个代码块并不容易，你不能直接传递代码块，因为Java是面向对象语言，你必须构造一个对象，这个对象的类需要有一个方法包含所需要的代码。然后传递一个对象。

  - `lambda表达式`是 Java语言 用来 **支持函数式编程 **的。

-  `lambda表达式` 表达的多样形式： 

  - 参数，箭头（->）以及一个表达式，并包含显式的 return 语句

  	```java
  	(String first, String second) ->
  		{
	    	if(first.length() < second.length()) return -1;
  	    	else if(first.length() > second.length()) return 1;
  	    	else return 0;
  		}
  	```
  	
  - 没有参数也要提供 空括号
  
    ```java
    () -> {for (int i = 100; i >= 0; i--) System.out.println(i);}
    ```
  
  - 如果可以推导出一个Lambda表达式的参数类型，则可以忽略其类型
  
    ```java
    Comparator<String> comp = (first, second) // same as (String first, String second)
        		-> first.length() - second.length();
    ```
  
  - 如果方法只有一个参数，而且这个参数的类型可以推导出，那么可以省略小括号
  
    ```java
    ActionListener listener = event ->
        System.out.println("The time is " 
          + Instant.ofEpochMilli(event.getWhen()));
    	// instead of (event) -> ... or (ActionEvent event) -> ...
    ```
  
  - 无需定义 `lambda表达式` 的返回类型，返回类型总是会由上下文推导得出。
  
    ```java
    (String first, String second) -> first.length() < second.length())
    ```
  
- **只有一个** 抽象方法 的接口，需要这种接口对象时，可以提供 一个`lambda表达式`，这种接口称为`函数式接口`。这个表达式会转化为接口，例子如下：

  ```java
  // 第二个参数 需要一个 Comparator实例（是只有一个方法的接口），可以提供一个 lambda表达式
  Arrays.sort(words, 
             (first, second) -> first.length() - second.length())
  ```

- `lambda表达式` 可以转化为 接口 。eg:

  ```java
  var timer = new Timer(100, event ->
      {
          System.out.println("At the tone, the time is" 
            + Instant.ofEpochMilli(event.getwhen()));
          Toolkit.getDefaultToolkit().beep();
      });
  ```

- 最好把 `lambda表达式` 看做是一个函数，而不是一个对象，另外要接受  `lambda表达式` 可以传递到函数式接口

- 实际上，在 Java中，对 `lambda表达式` 所能做的 **也只是** 转化为 `函数式接口`​。**​没有为 ​Java​语言 ​增加​函数​类型。**:imp:  :imp:  :imp:  

- `方法引用 ` : 例如下面的 `System.out::println` 就是一个方法引用，他指示 **编译器** 生成一个 **函数式接口**实例，用给定的方法覆盖实例的抽象方法并调用。 下面例子会生成 ActionListener对象, 它的  `actionPerformed(ActionEvent event)` 方法会调用 `System.out.println(e) `。

  ```java
  // 假设你希望只要出现一个定时器时间就打印这个事件对象
  var timer = new Timer(1000, event -> System.out.println(event));
  // 直接把 println方法 传递到 Timer构造器
  var timer = new Timer(1000, System.out::println);
  // 假设你想对字符串进行排序，而不考虑字母大小写。可以传递以下方法表达式
  Arrays.sort(strings, String::compareToIgnoreCase);
  ```

- `方法引用` 与 `lambda表达式` 类似，两者都不是对象。在为 `函数式接口` 的变量赋值时会生成一个对象（即方法引用不能独立存在，总是会转化为函数式接口的实例）。注意： 只有当 `lambda表达式` 的体只调用一个方法而不做其他操作时，才能把 `lambda表达式` 重写为 `方法引用`（阐述了两者的区别）:imp:  :imp:  :imp:  

- `方法引用`  主要有三种情况，要用 `::运算符` 分割方法名与类名或对象
  - object::instanceMethod
    - 等价于 `lambda表达式`   eg: `System.out::println` 等价于 `x -> System.out.println(x)`
  - Class::instanceMethod
    - 第一个参数会成为方法的隐式参数 eg: `String::compareToIgnoreCase` 等价于 `(x, y) -> x.compareToIgnoreCase(y)`
  - Class::staticMethod
    - 所有参数都会传递到静态方法中 eg：`Math.pow` 等价于 (x, y) -> Math.pow(x, y)

- 方法引用可以使用 this指参数，super也是合法的  eg: `this::equals` 等同于 `x -> this.equals(x)`

- `构造器引用` ： 与方法引用类似，只不用方法名为 `new`，eg: `Person::new` 是 person 构造器的一个引用

  ```java
  ArrayList<String> names = ...;
  Stream<Person> steam = names.stream.map(Person::new);
  List<Person> people = stream.collect(Collectors.toList());
  ```

- 可以用 数组类型 建立`构造器引用`。 eg: `int::new` 是一个构造器引用，他有一个参数：即数组的长度。这个引用等价于 lambda表达式 `x -> new int[x]`

-   `变量作用域` : 希望能够在 `lambda表达式` 中访问外围方法或类中的变量

  ```java
  public static void repeatMessage(String text, int delay)
  {
      ActionListener listener = event ->
      {
          System.out,println(text);
          Toolkit.getDefaultToolkit().beep();
      };
      new Timer(delay,listener).start();
  }
  ```

  - text 并不是在这个 `lambda表达式` 中定义的， `lambda表达式` 的代码可能会在 reapeatMessage 调用返回很久后才运行，而那时，这个参数变量 已经不存在了，如何保留呢？

    -   `lambda表达式`  有 3 个部分：
      - 一个代码块
      - 参数
      - **自由变量的值**，这是指非参数而且不在代码中定义的变量 eg： text
    - 这个  `lambda表达式`  的自由变量是 text。表示  `lambda表达式`  的数据结构必须会存储自由变量的值。我们说它被  `lambda表达式`  **捕获**（captured)  eg：可以把  `lambda表达式`  转换为包含一个方法的对象，这个 **自由变量** 的值就会复制到这个对象的实例变量中。

  - 要确保 捕获的值是明确定义的，这里有一个**重要限制**：在  `lambda表达式`  中，只能引用 **值不会改变** 的变量（原因之一：在  `lambda表达式`  中更改变了，在并发执行多个操作会不安全）

    - 如果这个变量在  `lambda表达式`  外可能改变，这也是 **不合法** 的，
    - 所 **捕获** 的变量必须是 `事实最终变量`:这个变量在初始化之后就不会在为它赋新值

  -   `lambda表达式` 体与嵌套块 有相同作用域。同样适用命名冲突和遮蔽的有关规则

    - 在  `lambda表达式`  中声明一个局部同名的参数 或 局部变量 是 **不合法** 的。在一个方法中，不能有两个同名局部变量，  `lambda表达式`  也不能有

    	```java
    	Path first = Path.of("/usr/bin");
    	// ERROR: Variable first already defined
    	Comparator<String> comp = 
    	    (first, second) -> first.length() - second.length();
	  	```
  
- 在  `lambda表达式`  中使用 this关键字，是指创建 这个  `lambda表达式`  的方法的 this参数

  ```java
  // 表达式 this.toString() 会调用 Application 对象的 toString 方法
  // 而不是 ActionListener实例的方法
  Public class Application{
      public void init(){
          ActionListener listener = event ->
          {
              System.out.println(this.toString());
              ...
          }
          ...
      }
  }
  ```

- 编写 自定义方法 处理  `lambda表达式` 

  - 使用 表达式的 重点： **延迟执行**

  - 之所以希望以后再执行，有很多原因，如：

    - 在一个单独的线程中运行代码
    - 多次运行代码
    - 在算法的适当位置运行代码，eg：排序中的比较操作
    - 发生某种情况时运行代码，eg：点击一个按钮，数据传达
    - 只在必要时运行代码

  - 例子：假设你想要重复一个动作 n 次，将这个动作和重复次数传递到一个 repeat 方法

    ```java
    repeat(10, () -> System.out.println("Hello,World!");
    // 接收 这个 lambda表达式 需要一个函数式接口
    public static void repeat(int n, Runnable action){
        for(int i = 0; i< n; i++) action.run();
    }
    
    // 如果我们希望告诉这个动作它出现在 哪一次迭代中，需要选择一个合适的函数式接口
    // 这个方法有一个int参数，且返回值为 void
    public interface IntConsumer{
        void accept(int value);
    }
    public static void repeat(int n, IntConsumer action){
        for(int i = 0; i < n; i++) action.accept(i);
    }
    repeat(10, i -> System.out.println("Countdown:" + (9 - i)));
    ```

- 如果设计你自己的接口，其中只有一个抽象方法，可以用注解 `@FunctionalInterface` 来标记，如果你无意中增加了另一个抽象方法，编译器会产生一个错误消息

## 6.3 内部类

- `内部类` ： 定义在另一个类中的类

- 为什么需要？
  - 内部类可以对同一个包中的其他类隐藏
  - 内部类方法可以访问定义这个类的作用域中的数据，包括原本私有属性
  
- Java 中 内部类 与 C++ 中嵌套类有一定区别
  - Java 内部类的对象会有一个 **隐式索引** ，指向实例化这个对象的外部类对象
  - Java 中静态内部类没有这个附加指针，相当于 C++ 中的嵌套类
  
- 举个例子

  ```java
  public class TalkingClock{
      private int interval;
      private boolean beep;
      
      public TalkingClock(int interval, boolean beep){ ... }
      public void start(){...}
      // an inner class
      
      public class TimerPrinter implememts ActionListener{
          ...
      }
  }
  
  public class TimerPrinter implememts ActionListener{
          public void actionPerformed(ActionEvent event){
              System.out.println("At the tone, this time is " +        
                 Instant.ifEpochMilli(event.getwhen));
              if(beep) Toolkit.getDefaultToolkit().beep();
          }
      }
  ```

  - 一个内部类方法 可以访问自身数据字段， 也可以访问创建它的外围类对象的数据字段
  - 内部类对象 总有一个 **隐式引用**， 指向创建它的外围类对象，它是不可见的，由 **编译器** 负责自动创建

- 内部类有一个外围类的引用（隐式引用），使用外围类引用的正规语法： `OutClass.this`

  - 可以这样改写 TimerPrinter类 的 actionPerformed 方法：

    ```java
     public void actionPerformed(ActionEvent event){
                ...
                if(TalkingClock.this.beep) Toolkit.getDefaultToolkit().beep();
            }
    ```

- 编写内部类对象构造器的明确语法： `outerObject.new InnerClass(construction parameters)`
	- 外围类引用 被设置为 内部类对象 的方法的 this引用， 通常 this限定词 多余
  	```java
  	ActionListener listener = this.new TimerPrinter();
  	```
  	
  - 显示将 外围类引用 设置为其他的对象，因为对于公共内部类，任何 外部类对象 都可以构造 内部类对象
  
    ```java
    var jabberer = new TalkingClock(1000, true);
    TalkingClock.TimePrinter listener = jabberer.new TimePrinter();
    ```
  
- 外围类作用域之外，引用内部类： `OuterClass.InnerClass`

- 内部类声明的 所有静态字段 **都必须** 是final，并初始化为一个编译时常量

- Java语法规范限制：内部类不能有 static 方法

- 内部类 是一个 **编译器现象**，与虚拟机无关。编译器会把内部类转化为 常规类文件， 用 $ 符分隔外部类名与内部类名，而虚拟机对此一无所知 eg： `TimePrinter类` 将被转化为成类文件 `TalkingClock$TimePrinter.class` ，内部类会存在 安全风险 :imp:  :imp:  :imp:   

- `局部内部类`： 如果内部类只是在外围类中使用 一次，出现这种情况，可以在 **一个方法中局部地 **定义这个类

  ```java
  public void start(int interval, boolean beep){
      class TimerPrinter implememts ActionListener{
          public void actionPerformed(ActionEvent event){
              System.out.println("At the tone, this time is " +        
                 Instant.ifEpochMilli(event.getwhen));
              if(beep) Toolkit.getDefaultToolkit().beep();
          }
          var listener = new TimerPrinter();
          var timer = new Timer(interval, listener);
          timer.start();
  }
  ```

  - 声明 局部内部类 不能有访问说明符
  - 作用域： 被限定在声明这个局部内部类的块中
  - 优势： 对 外部世界 完全隐藏，甚至 外围类 中的其他代码也不能访问它
  - 优点：他们不仅能够访问外部类的字段，还可以访问局部变量（必须是事实最终变量），在编译器底层会为这个局部变量创建相应实例字段，并把局部变量复制到构造器（防止方法结束，局部变量消失）

- `匿名内部类`： 只想创建这个类的一个对象，甚至不想要为类指定名字

  ```java
  public void start(int interval, boolean beep){
          var listener = new ActionListener{
          public void actionPerformed(ActionEvent event){
              System.out.println("At the tone, this time is " +        
                 Instant.ifEpochMilli(event.getwhen));
              if(beep) Toolkit.getDefaultToolkit().beep();
          };
          var timer = new Timer(interval, listener);
          timer.start();
  }
  ```

  - 这个语法非常晦涩难懂， 含义：创建一个类的新对象，这个类实现了 ActionListener 接口，需要实现的方法在 actionPerformed 中定义
  
- 语法：
  
    ```java
    new SuperType(construction parameters){
        inner class methods and data
    }
    ```
    
    - `SuperType` 是 接口，如果是这样，内部类就要实现这个接口 eg: ActionListener
    - `SuperType` 是 类，如果是这样，内部类就要扩展这个类
    
    - **匿名内部类不能有构造器**，因为构造器名字必须与类名相同，而匿名内部类没有类名 :imp:  :imp:  :imp:   
    
    - `construction parameters` 构造参数 是要传递给超类构造器的变量，如果一个内部类实现一个接口，那就不会有任何构造参数( 接口是定义行为的，不是定义生产方式的 )，不过仍然要 提供一个小括号
    
      ```java
      new InterfaceType(){
          methods and data
      }
      ```
    
  - 例子: 类构造新对象 和 扩展了那个类的匿名内部类对象 之间的差别
  
    ```java
    // a Person Object
    var queen = new Person();
    // an object of an inner class extending Person
    var count = new Person("Dracula"){...};
    ```
  
    - 如果 构造参数列表 后跟一个开始大括号，就是定义 `匿名内部类`
  
  - 尽管不能有构造器，但可以提供一个对象初始化块
  
    ```java
    var count = new Person("Dracula"){
        {Initialization}
        ...
    };
    ```
  
  - Java程序员习惯使用匿名内部类实现 事件监听器 和 其他回调，如今,还是使用 `lambda表达式`
  
    ```java
    public void start(int interval, boolean beep){
            var timer = new Timer(interval, event -> {
                System.out.println("At the tone, this time is " +        
                   Instant.ifEpochMilli(event.getwhen));
                if(beep) Toolkit.getDefaultToolkit().beep();
            });
            timer.start();
    }
    ```
  
- `静态内部类`： 只是想为了把一个类隐藏在另外一个类的内部，并不需要内部类有外围类对象的一个引用。将内部类声明为 `static` ，这样就不会生成那个引用（外围对象引用）

- 如果 内部类对象是 在静态方法中创建 ，那这个内部类 必须是静态内部类 :imp:  :imp:  :imp:   

    - 原因： 静态方法不能访问对象，因为静态方法执行时，这个对象可能还没有创建，如果创建普通内部类，他会有外围类对象的引用，但是在实际执行这个静态方法的时候，编译器不知道是否已经创建了这个对象，所以，编译器不知道你产生外围类对象引用是否不合理，所以会报错

- 在接口中声明的内部类自动是 static 和 public

## 6.4 服务加载器

- `ServiceLoader类`

## 6.5 代理

- `代理`： 利用代理可以在 运行时 创建实现了一组给定接口的新类，只有在编译时期无法确定需要实现哪个接口时才有必要使用代理

***目前不重要，留着以后看***  *page273*

# 第七章 异常、断言和日志

## 7.1 处理异常

- ~~如果由于出现错误使得某些操作没有完成， 程序应该：~~
  
  - ~~返回到一种安全状态，并能够让用户执行其他命令~~
  - ~~允许用户保存所有工作的结果，并以妥善的方式终止程序~~
  
- ~~异常处理的任务：将控制权从产生错误的地方转移到能够处理这种情况的错误处理器~~

- ~~必须考虑到的程序中可能出现的异常：~~
  
  - ~~用户输入错误~~
  - ~~设备错误~~
  - ~~物理限制~~
  - ~~代码错误~~
  
- 如果某个方法不能够采用正常途径完成它的任务，可以通过另外一个路径退出方法，抛出（throw）一个**封装了错误信息的“对象”**，这个方法会立即退出，取而代之，异常处理机制 开始搜索能够处理这种异常状况的 异常处理器

- 在 Java程序设计语言中，异常对象 都是派生于 `Throwable类` 的一个类实例

- 异常层次结构简化图
  ```mermaid
  graph TD
      	B["Throwable"]
      	B-->C[Error]
      	B-->D(Exception)
      	D-->E(IOException);
      	D-->F(Runtime Exception);
  ```

  - `Error类`：Java 运行时系统的 内部错误 和 资源耗尽错误，你的程序不应该抛出这种异常对象
  - `RuntimeException类`： 由编程错误导致的异常
  - `IOException类`： 由于I/O错误这类问题导致的异常
  - 派生于 `RuntimeException` 的异常包括以下几个问题：
    - 错误的强制类型转换
    - 数组访问越界
    - 访问null指针
  - 不是派生于`RuntimeException类` 的异常 (其他异常) 包括：
    - 试图超越文件末尾继续读取数据
    - 试图打开一个不存在的文件
    - 试图根据给定的字符串查找Class对象，而这个字符串表示的类并不存在

- Java语言规范 将派生于 `Error类` 和 `RuntimeException类` 的所有异常称为 `非检查型异常`，包括 `IOException类` 在内的所有 **其他的异常** 称为 `检查型异常`

  - 编译器将检查你是否为所有的 `检查型异常` 提供了异常处理器

- ~~遇到下面两种情况，要告诉调用这个方法的程序员有可能抛出的异常~~
  - ~~调用了一个抛出 检查型异常 的方法，eg：`FileInputStream 构造器`~~
  - ~~检测到一个错误，并且利用 throw 语句抛出一个 检查型异常~~

- 一个方法必须声明所有可能抛出的 `检查型异常`， 而 `非检查型异常` 要么在你的控制之外(Error)，要么是由从一开始就应该避免的情况所导致的(RuntimeException)。如果你的方法没有声明所有可能发生的 `检查型异常`， **编译器** 就会发出一个错误消息

- 在子类中覆盖了一个超类方法， 子类方法中声明的 `检查型异常` 不能比超类方法中声明的异常更通用(抛出更特定的异常或者不抛出)
- 如果超类方法没有抛出任何 `检查型异常` ， 子类也不能抛出任何 `检查型异常`  :imp:  :imp:  :imp:  

- 如果类中的一个方法声明他会抛出一个异常，而这个异常是某个特定类的实例，那么这个方法抛出的异常可能属于这个类，也可能属于这个类的任意一个子类

- Java中 `throws说明符` 在编译时执行，C++ 在运行时执行

- 抛出一个异常的语法：

  ```java
  // 以 EOFException 为例
  
  // 1.
  throw new EOFException();
  // 2. 
  var e = new EOFException();
  throw e;
  
  // 将上面这些代码放在一起
  String readData(Scanner in) throws EOFException{
      ...
      while(...)
      {
          if(!in.hasNext()) // EOF encountered
          {
              if(n < len){
                  throws new EOFException();
              }
          }
          ...
      }
      return s;
  }
  
  // 利用 EOFException构造器，更细致描述这个异常
  String gripe = "Content - length: " + len + ", Received" + n;
  throw new EOFException(gripe);
  ```

- ~~已经有异常类可以满足需求，如何抛出~~

  - ~~找到合适的异常类~~
  - ~~创建这个类的一个对象~~
  - ~~将对象抛出~~

- 创建异常类：任何标准异常类都无法描述清楚的问题

  - 自定义一个 派生于 `Exception类` 或者 派生于 `Exception类` 的某个子类的类

  - 习惯自定义的这个类包含两个构造器

    - 默认构造器
    - 包含详细描述信息的构造器（超类 Throwable 的 toString方法 会返回一个字符串，包含这个详细信息）

  - 例子

    ```java
    class FileFormatException extends IOException{
        public FileFormatException(){}
        public FileFormatException(String gripe){
            super(gripe);
        }
    }
    // 抛出你自定义的异常类型
    String readData(BufferedReader in) throws EOFException{
        ...
        while(...)
        {
            if(ch = -1) // EOF encountered
            {
                if(n < len){
                    throws new FileFormatException();
                }
            }
            ...
        }
        return s;
    }
    ```

## 7.2 捕获异常

- 如果发现异常，没有捕获，程序会终止，并在控制台上打印一个消息： 这个异常的类型 + 一个 **堆栈轨迹**

-  想要捕获一个异常，需要设置 `try/catch语句块`

  - 最简单的 try 语句块

    ```java
    try{
    	code
        more code 
        more code
    }catch (ExceptionType e){
        handler for this type
    }
    ```

  - 如果 try 块中的任何代码抛出 catch子句 中 指定的一个异常类，那么

    - 程序将跳过 try语句块中的其余代码
    - 程序将执行 catch子句中的处理器代码
  - try块没抛出任何异常，会跳过catch子句
  - 抛出了catch子句中没有声明的一个异常类型，方法会立即退出

- 一般情况，调用了一个抛出检查型异常的方法，可以继续抛出去，也可以捕获，但是也有特例：你编写的一个 **覆盖** 超类的方法，如果这个超类没有抛出异常，你就 **必须** 捕获你的方法代码中出现的每一个检查型异常。**不允许出现子类的 throws说明符 中出现超类方法未列出的异常**   :imp:  :imp:  :imp:  

- `try语句块`： 中可以捕获多个异常类型，并对不同类型的异常做出不同的处理

  ```java
  // 例子
  try{
  	code that might throw exceptions 
  }catch(FileNotFoundException e)
  {
      emergency action for missing files
  }catch(UnknownHostException e)
  {
      emergency action for unknown hosts
  }catch(IOException e)
  {
      emergency action for all other I/O problems
  }
  ```

- 可以使用 `e.getMessage()` , 获得详细的错误消息(如果有)

- 得到异常对象的实际类型： `e.getClass().getName()`

- 同一个 catch子句 可以捕获多个异常   Java7 后

  ```java
  // 假如对应缺少文件 和 未知主机异常 的 动作是一样的
  try{
  	code that might throw exceptions 
  }catch(FileNotFoundException | UnknownHostException e)
  {
      emergency action for missing files and unknown hosts
  }
  ```

  - 这种语法限制：捕获类型彼此之间不存在 子类关系
  - 这种同时捕获多个异常，声明的 异常变量对象 是 final 类型的，不能赋不同的值

- 再次抛出异常与异常链： 通常希望改变 异常的类型 时，可以在 catch子句 中抛出一个异常

  ```java
  // 执行一个 servlet 代码，可能不想知道发生错误的细节，但希望明确地知道 servlet 是否有问题
  try{
  	access the database
  }catch(SQLException e)
  {
      // 构造 ServeletException 时，提供了异常的消息文本
      throw new ServeletException("database error");
  }
  
  // 一个更好的处理方法：把原始异常设置为 新异常的原因（包装技术）
  try{
  	access the database
  }catch(SQLException original)
  {
      var e = new ServeletException("database error");
      e.initCause(original);
      throw e;
  }
  // 捕获到异常以后，使用下面语句获取原始异常(估摸 Cause 是个新定义的字段)
  Throwable original = caughtException.getCause();
  // 有时只是记录，再重新抛出
  try{
  	access the database
  }catch(Exception e)
  {
      logger.log(level, message, e);
      throw e;
  }
  ```

- 一个方法发生一个 检查性异常，但这个方法不允许抛出检查型异常，那 **包装技术** 很好用，捕获检查型异常，并将其包装成一个运行时异常

- `finally子句`： **不管是否有异常被捕获， finally子句中的代码都会执行**（经常放，清理 终止方法获得的本地资源的代码）

  ```java
  var in = new FileInputStream(...);
  try{
      // 1
      code that might throw exceptions
      // 2
  }catch(IOException e){
      // 3
      show error message
      // 4
  }finally{
      // 5
      in.close();
  }
  	// 6
  
  // 代码抛出异常，catch子句 抛出异常，异常将抛回这个方法的调用者，执行顺序只是：1、3、5
  
  // 代码抛出异常，没有任何 catch子句 捕获这个异常，执行try中语句直到抛出异常，跳过剩余代码，
  // 然后执行finally子句中语句，并将异常抛回给方法的调用者 执行顺序只是：1、5
  ```
  - try 语句 可以只有 finally子句，而没有catch子句

- try-finally还可以嵌套在 try-catch 中

  ```java
  InputStream in = ...;
  // 内层职责：关闭输入流
  // 外层职责：确保报告出现的错误
  // 优势：还会报告 finally子句中出现的错误
  try{
      try{
          code that might throw exceptions
      }finally{
          in.close();
      }
  }catch(IOException e){
      show error message
  }
  ```

- `finally子句` 的体 要 **用于清理资源**，不要把改变控制流语句(return，throw，break， continue)放在 `finally子句` 中  :imp:  :imp:  :imp:  

- `try-with-Resources子句 `： java7 开始

  - 假设 **资源属于实现**  `AutoCloseable接口` 的类，`AutoCloseable接口` 有一个方法： `void close throws Exception`， `Closeable接口`是它的子接口，抛出的是 `IOException`

  - try-with-Resources子句 (带资源的try语句) 的最简形式：

    ```java
    try(Resource res = ...)
    {
        work with res
    }
    ```

    - try块退出时，会自动调用 `res.close()`

  - 例子：

    ```java
    // 这个块正常退出时，或者存在一个异常时，都会调用 in.close() 方法，就好像使用了 finally块 一样
    try(var in = new Scanner(
        new FileInputStream("/usr/share/dict/words"), StandardCharsets.UTF_8)
    {
        while(in.hasNext()) 
            System.out.println(in.next());
    }
    
    // 还可以指定多个资源
    try(var in = new Scanner(
        new FileInputStream("/usr/share/dict/words"), StandardCharsets.UTF_8;
        var out = new PrintWriter("out.txt", StandardCharsets.UTF_8))
    {
        while(in.hasNext()) 
            System.out.println(in.next());
    }    
    // 不论 这个块 如何退出， in 和 out 都会自动关闭
    ```
  
- Java9 中可以在  try首部 中提供之前声明的 事实最终变量

  ```java
  public static void printAll(String[] lines, PrintWriter out){
      try(out){ //effectively final variable
          for(String line : lines)
              out,println(line);
      } // auto out.close called here
  }
  ```

- **只要需要关闭资源，就要尽可能使用** `try-with-Resources语句`， `try-with-Resources语句` 自身也可以有 catch子句，甚至还可以有 finally子句。这些 子句 会在关闭资源之后执行

- `堆栈轨迹`: 程序执行过程中 某个特定点上， **所有挂起方法调用** 的一个列表
  - 可以调用 `Throwable类` 的 `printStackTrace 方法` 访问堆栈轨迹的文本描述信息

 ## 7.3 使用异常的技巧

- 异常处理不能代替简单的测试
  - 基本原则：只在异常情况下使用异常
- 不要过分的细化异常： 不要每一句一个 try
- 充分利用异常层次结构
  - 不要只抛出 `RuntimeException` 异常，应寻找一个 合适的子类，或者创建自己的异常类
  - 不要只捕获 `Throwable` 异常
  - 如果能够将有一种异常 转化为另一种更加适合的异常，那么不要犹豫

- 不要压制异常，例如这样： `try{...}catch(Exception e){}`
- 在检测错误时，苛刻比放任更好
- 不要羞于传递异常

## 7.4 使用断言

- `断言机制`： 允许在 **测试期间** 向代码中插入一些检查， 而在产生代码中会自动 删除这些检查

- 引入关键字 `assert` ，两种语法形式：两种语句都会计算条件，如果为 false 就会抛出 `AssertionError` 异常

  - `assert condition;`
  - `assert condition:expression; `
    - 表达式(expression)：将传入 `AssertionError` 对象的构造器，并转换成一个消息字符串，该部分唯一目的：产生一个消息字符串，并不存储具体的消息表达值

  ```java
  // 想断言 x 是一个 非负数
  assert x >= 0;
  // 将 x 的实际值 传递给 AssertionError对象,以便以后显示
  assert x >= 0: x;
  ```

- **默认 断言 是禁用的**， 可以在运行程序时 用  `-enableassertions` 或 `-ea` 选项启用 eg： `java -enableassertions MyApp`

- 启用 或者 禁用 断言 是 `类加载器` 的功能

  - 禁用断言，类加载器会去除断言代码， 因此，**不会** 降低程序运行速度 :imp:  :imp:  :imp:  
  - 可以在 某个类 或者 整个包中 启用断言 eg:  `java -ea:MyClass -ea:com.mycompany.mylib MyApp`
  - 可以用选项 `-disableassertions` 或 `-da` 在某个特定类 和 包中禁用断言 eg: `java -ea:... -da:Myclass MyApp`
  - 启用和禁用所有断言的 `-ea` 和 `-da`  开关不能应用到那些没有 类加载器 的 “系统类”上，对这些类，要用`-enablessystemassertions/-esa` 开关启用断言
  - 可以通过 编程控制 类加载器(java.lang.ClassLoader) 的状态

- Java语言中，给出了3种 处理系统错误的机制：
  - 抛出一个异常
  - 日志
  - 使用断言
- 什么时候选择 使用 `断言` ？
  - 断言是致命的、不可恢复的错误
  - 断言是 只在开发 和 测试阶段打开
  - 断言只应该用于在 测试阶段 确定 程序内部错误 的位置

- `断言` 是一种 **测试** 和  **调试** 阶段 使用的 战术性工具，`日志` 是在 **程序整个生命周期** 都可以使用的 战略性工具

## 7.5 日志

- 基本日志：要生产简单 日志记录， 可以使用 `全局日志记录器  `  (global logger) 并调用 `info方法`

  ```java
  Logger.getGlobal().info("File->Open menu item selected");
  // 默认情况下，会如下打印这个记录
  May 10, 2013 10:12:15 PM LoggingImageViewer fileOpen
  INFO: File->Open menu item selected
      
  // 在适当地方（如 main 前）调用 下方法，会取消所有日志
  Logger.getGlobal().setLevel(Level.OFF);
  ```

- 行业级日志：在一个专业应用程序中，你肯定不想将所有的日志都记录到一个 `全局日志记录器 `  中，可以定义自己的日志记录器

  - 调用 `getLogger` 方法创建 或 获取 日志记录器

    ```java
    // 使用 静态变量 存储日志记录器的 引用， 为了防止未被任何变量引用的 日志记录器 被垃圾回收
    private static final Logger mylogger = Logger.getLogger("com.mycompany.mayapp");
    ```


- `日志记录器名` 与 `包名`

  - 两者都具有 层次结构，但日志记录器层次更强
  - 包 与 父包之间没有语义关系，日志记录器的父与子 之间将共享某些属性 eg： 对一个日志记录器设置级别，子日志记录器也会继承这个级别

- 日志记录器的级别： 高 --> 低

  - SEVERE
  - WARNING
  -  INFO
  - CONFIG
  - FINE
  - FINER
  - FINEST

- 默认情况下，日志记录器只记录 前 3 个级别，可以设置不同级别 eg: 

  ```java
  // FINE以及所有更高级别日志会被记录
  logger.setLevel(Level.FINE);
  ```

- 开启所有级别日志记录 ： `Level.ALL` ,关闭所有级别日志记录：`Level.OFF`

- 所有级别都有 日志记录方法

  ```java
  logger.warning(message);
  logger.fine(message);
  ```

- 日志记录 还可以 使用 `log方法` 并指定级别

  ```java
  // 记录又给定级别、消息 的日志记录 可包含对象 或者 可抛出对象
  logger.log(Level.FINE, message);
  ```

-  默认的日志记录将显示：根据 调用堆栈 得出的 类名和方法名（包含日志调用）

- 可以使用 `logp方法` 获取调用类和方法的确切位置

  ```java
  // 记录又给定级别、准确调用者、消息 的日志记录 可包含对象 或者 可抛出对象
  void logp(Level l, String className, String methodName, String message)
  ```
  
- 一些用来跟踪执行流的便利方法

  ```java
  // 记录一个 描述 进入/退出 的方法(有给定参数和返回值) 的日志记录
  void entering(String className, String methodName)    
  void entering(String className, String methodName, Object param)
  void entering(String className, String methodName, Object[] params)
  void exiting(String className, String methodName)
  void exiting(String className, String methodName, Object result)    
  
  // 以下例子 会生成 FINER级别， 以 字符串 ENTRY 和 RETURN 开头的日志记录
  int read(String file, String pattern){
      logger.entering("com.mycompany.mylib.Reader", "read", new Object[]{ file, pattern});
      ...
      logger.exiting("com.mycompany.mylib.Reader", "read", count);
      return count;
  }
  ```

- 使用以下两个方法，在日志记录中包含异常描述。这是日志记录常见的用途

  ```java
  void throwing(String className, String methodName, Throwable t)
  void log(Level l, String message, Throwable t)
  // throwing 调用 可以记录一条 FINER级别日志记录 和一条以 THROW 开头的消息
  if(...){
      var e = new IOException("...");
      logger.throwing("com.mycompany.mylib.Reader", "read", e);
      throw e;
  }
  
  try{
      ...
  }catch(IOException e){
      Logger,getLogger("com.mycompany.myapp").log(Level.WARNING, "Reading image", e);
  }
  ```

  

