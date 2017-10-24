# Kotlin入门学习第一天
## 学习内容：Kotlin基础
1. kotlin课程简介
2. kotlin开发工具
3. helloworld
4. 基本数据类型
5. 字符串和元组数据
6. 输出函数和输入函数
7. 变量和不可变变量以及智能类型推断 
8. 数据类型转换

## 学习存疑
无

## 01.Helloworld
```
fun main(args: Array<String>) {
    println("Hello, world!")
}
```
## 02.01基本数据类型
```
fun main(args: Array<String>) {
    //var + 关键字 + ： +变量类型
    var a:Boolean = true
    var b:Byte = 10
    var short:Short = 20
    var char:Char = 'a'
    var i:Int = 10
    var f:Float = 10.123456789F //必须加F
    var d:Double = 1.123456789123456789
    var l:Long = 10L //不必须加L
}
```
## 02.02.基本数据类型和java比较
```
fun main(args: Array<String>) {
    var a:Int = 10 //自动选择使用java基本数据类型
    a.hashCode() //自动选择使用Integer
}
```
查看kotlin对应的java代码
Tools -> Kotlin -> Show Kotlin Bytecode -> Decomplie
```
public final class _02_02_基本数据类型和java的对比Kt {
   public static final void main(@NotNull String[] args) {
      Intrinsics.checkParameterIsNotNull(args, "args");
      int a = 10;
      Integer.valueOf(a).hashCode();
   }
}
```
## 02.03.kotlin调用java
kotlin100%支持java，因此可以使用java中的包

eg. kotlin使用java的高精度浮点数
```
import java.math.BigDecimal

fun main(args: Array<String>) {
    var f = 1.123456789123456789f
    println(f)
//    BigDecimal big1 = new BigDecimal("1.123456789123456789"); //java写法
    var big2:BigDecimal = BigDecimal("1.123456789123456789")
    println(big2)
}
```
## 02.04.基本数据类型的取值范围
Range of Byte:-128 ... 127

Range of Short:-32768 ... 32767

Range of Byte:-2147483648 ... 2147483647

Range of Byte:-9223372036854775808 ... 9223372036854775807

Range of Byte:-1.4E-45 ... 3.4028235E38
```
fun main(args: Array<String>) {
    var maxB:Byte = Byte.MAX_VALUE
    var minB:Byte = Byte.MIN_VALUE
    println("Range of Byte:${minB} ... ${maxB}")

    var maxS = Short.MAX_VALUE
    var minS = Short.MIN_VALUE
    println("Range of Short:${minS} ... ${maxS}")

    var maxI = Int.MAX_VALUE
    var minI = Int.MIN_VALUE
    println("Range of Byte:${minI} ... ${maxI}")

    var maxL = Long.MAX_VALUE
    var minL = Long.MIN_VALUE
    println("Range of Byte:${minL} ... ${maxL}")
    
    var maxF = Float.MAX_VALUE
    var minF = Float.MAX_VALUE//对应的并不是最小值
    var minF2 = -Float.MIN_VALUE
    var a = Float.MIN_VALUE
//    println("Range of Byte:${minF} ... ${maxF}")
    println("Range of Byte:${minF2} ... ${maxF}")
}
```
## 03.智能类型推断和类型转换
声明变量时如果没有指定数据类型，kotlin会根据后面初始化的数据来自动判断数据类型

kotlin有变量类型安全，会拒绝给该变量赋值其他数据类型的值
```
fun main(args: Array<String>) {
    var a = 10
    a = 20
//    a = "abc"  错误
    //kotlin变量类型安全

    var b:Int = 10
    var c:Long =20
    b = c.toInt()
}
```
## 04.01.可变变量和不可变变量
var 可变变量 (variable)

val 不可变变量 (value)  相当于JAVA中的final
```
fun main(args: Array<String>) {
    var a = 10
    a = 20

    val b = 10
//    b = 20 错误
}
```
## 05.01.字符串
字符串用一对双引号包括，用法和JAVA一样，同样也可以用转义字符

kotlin中新添加了一种格式---""" """前后分别三个双引号包括一段话

其间的内容原样输出，包括换行等格式

备注：其间断行后的内容不需要缩进  即每行前面缩进了多少空格就会原样输出多少
```
fun main(args: Array<String>) {
    //定义字符串
    var s:String = "中国\n广东省\n深圳"
    println(s)
    //原样输出字符串
    var ss = """中国
广东省
深圳市"""
    println(ss)
}
```
## 05.02.字符串删除空格
trim()删除行前空格
trimMargin("|")删除行前后空格以及行前"|"字符
```
fun main(args: Array<String>) {
    val str1 = "   asdfgh   "
    println(str1)
    println(str1.trim())
    /**
     *    asdfgh
     *asdfgh
     */
    val str2 = """中国
    |广东省
    |深圳"""
    println(str2)
    println(str2.trimMargin("|"))
    /**
     * 中国
     *     |广东省
     *     |深圳
     *中国
     *广东省
     *深圳
     */
}
```
## 05.03.字符串比较
在kotlin中 == 运算符和equals函数一样，比较两个字符串内容是否相同

而 === 运算符比较的是两个字符串的引用是否相同

其中通过s1和s3的比较与s1和"hello"的比较可以看出，相同的字符串引用是相同的（同一个对象）
```
fun main(args: Array<String>) {
    var s1 = "hello"
    var s2:String = String(charArrayOf('h','e','l','l','o'))
    var s3 = "hello"
    
    println(s1) //hello
    println(s2) //hello
    println(s1.equals(s2)) //true
    println(s1 == s2) //true 和equles一样
    println(s1 === s2) //false 比较字符串引用地址
    println(s1 === s3) //true
    println(s1 == "hello") //true
    println(s1 === "hello") //true
}
```
## 06.元组数据
二元元组  Pair 保存两个数据

三元元组 Triple 保存三个数据

相当于只有两个值或者三个值的数组，但是实际用起来却方便许多
```
fun main(args: Array<String>) {
    //二元元组
    val pair = Pair("张三",20)
    println(pair.first)
    println(pair.second)

    //三元元组
    val triple = Triple("李四",30,"134455")
    println(triple.first)
    println(triple.second)
    println(triple.third)
}
```
## 07.空值处理
?.空安全调用符号，如果s为空不执行后面toInt，不为空才执行

!!.非空断言 告诉编译器一定不为空，如果为空则运行时扔会报错

String 不可空数据类型     String?可空数据类型，两者虽然都是储存字符串但是不是相同类型

其他数据类型相同

eg. var a:Int = s?.toInt() 类型不匹配异常，需要一个Int类型但找到的是一个Int?类型

eg. s!!.toInt() 可以运行，但是运行时会报空指针异常，程序中断
```
fun main(args: Array<String>) {
    var s:String? = null
    //将String字符串转化为Int
    //由于s是可空数据类型，直接调用可能造成空指针异常，编译器不能便宜通过
    s?.toInt()
    println(s?.toInt())
    var a:Int = s?.toInt()?:-1
    //s不为空就把s.toInt()传递给a，如果为空就把-1赋值给a
}
```
## 08.输入函数和输出函数
输出函数中内容由一对双引号包括，其间内容原样输出

要输出变量值的话可以用 **${变量名}** 或者 **$变量名** 方式加入双引号中

readLine()会把输入数据以字符串形式读入
```
fun main(args: Array<String>) {
    //输出函数
    var a = 10
    var b = 20
    println(a)
    println("a=${a},b=$b")
    //输入函数
//    var s:String //非空类型
    var s:String?
    var c:Int
    s = readLine()//读取数据
    println(s)
}
```

## 作业

### 1
大家来找碴,找出下列代码的错误：

```
/*
 * 常见错误
 */
fun main(args: Array<String>) {
    val title: String   //声明变量title存储课程名
    println(title)      //从控制台输出变量的值
```
答：

title为不可变变量，必须要进行初始化

或者title声明为可变变量，然后通过输入函数或者直接赋一个值

之后才能够用println()输入
```
funmain(args:Array＜String＞){
vartitle:String="Kotlin入门"//声明变量title存储课程名
println(title)//从控制台输出变量的值
}
```
### 2
大家来找碴,找出下列代码的错误：

```
/*
 * 常见错误
 */
fun main(args: Array<String>) {
    val name = "张三"    //声明变量存储“张三”
    val name = "李四"    //声明变量存储“李四”
}
```
答：

变量不能重名
```
funmain(args:Array＜String＞){
    valname1="张三"//声明变量存储“张三”
    valname2="李四"//声明变量存储“李四”
}
```
### 3
请输出个人档案，做自我介绍

```
funmain(args:Array＜String＞){
    varintroduce:String="""姓名：李木一
    年龄：22
    地址：内蒙古自治区包头市
    性别：男"""
    println(introduce)
}
```

### 4
通过编程实现，交换两个整数,第一个整数是first = 10 ，第二个整数是second = 8，第三个整数是临时变量third，首先打印出来交换前的数据，然后打印交换之后的数据。

```
funmain(args:Array＜String＞){
    varfirst:Int=10
    varsecond:Int=20
    varthird:Int
    println("first=${first}second=${second}")
    third=first
    first=second
    second=third
    println("first=${first}second=${second}")
}
```
