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

- 如果是用较短的字符串构建字符串用 StringBuilder构建，如果是更偏于共享就直接用string类

  - StringBuilder
    - append()
    - toString()

  - StringBulider 的前身StringBuffer 效率低，但可采用多线程执行，如果在单线程执行用 StringBuilder

## 3.7 输入与输出

