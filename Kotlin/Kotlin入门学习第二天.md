# Kotlin入门学习第二天

## 学习内容：函数和控制语句
1. 函数入门和加强
2. 字符串模板
3. 空值处理
4. if条件控制语句
5. 流程控制语句for以及range
6. 流程控制语句while
7. 数组

## 学习存疑
1. 声明变量省略类型时idea不能显示Kotlin推断的类型
2. 05.03.反向区间和区间的反向 直接定义val range:IntProgression = 10..1 为什么不能用forEach遍历

## 01.四种函数

```
fun main(args: Array<String>) {
    sayHello()
    sayHello("张三")
    var length = getNameLength("张三")
    println(length)
    haha()
}
//打印hello
fun sayHello() {
    println("hello")
}
//传入name hello name
fun sayHello(name:String) {
    println("hello $name")
}
//传入name hello name 返回名字的字数
fun getNameLength(name:String):Int {
    return name.length
}
//没有参数返回
fun haha():String {
    return "haha"
}
```
## 02.字符串模板

```
fun main(args: Array<String>) {
    var name = "小吴"
    var place = "中国"
    var age = 20
    var job = "老师"

    val s:String = introduce(name,place,age,job)
    println(s)
}
fun introduce(name:String,place:String,age:Int,job:String):String {
    return "我是$name 年龄$age 来自$place 工作是$job"
}
```
## 03.01.for循环
两种形式

for(**变量名** in **遍历变量/常量**){ }

for((**下标变量名**,**变量名**) in **遍历变量/常量**.withIndex()){ }

```
fun main(args: Array<String>) {
    val s = "我是中国人"
    //将字符串所有字符找到并打印
    for(c:Char in s) {
        println(c)
    }
    for((index,c) in s.withIndex()) {
        println("位置=$index ,字符=$c")
    }
}
```
## 03.02.forEach高级for循环

**遍历变量/常量**.forEach {//it储存着每个元素}

s.forEachIndexed { **下标变量名**, **变量名** -> }

```
fun main(args: Array<String>) {
    val s = "我是中国人"
    //将多有字符打印
    s.forEach {
        println(it) //it代表每一个元素
    }
    s.forEachIndexed { index, c ->
        println("位置=$index ,字符=$c")
    }
}
```
## 03.03.for循环continue和break

 * break 跳出循环
 * continue 跳过本次循环
 * return 跳出方法

```
fun main(args: Array<String>) {
    var s = "abcde"
    for (c in s) {
        if(c == 'c') {
//            break         //输出a b
//            continue      //输出a b d e
//            return        //输出a b
        }
        println(c)
    }
    println("方法执行结束了")
}
```
## 03.04.标签处返回

break 只能跳出直接包含它的那层循环

在Kotlin中可以在外层循环前用 **标记名+@** 标记一个循环再在break后跟上 **@+标记名** 表示该break跳出的是哪层循环

```
fun main(args: Array<String>) {
    val s1 = "abc"
    val s2 = "123"
    loop@for(c1 in s1) {
        for(c2 in s2) {
            if(c1 == 'b' && c2 == '2') {
                break@loop
            }
            println("$c1 $c2")
        }
    }
}
```
不用标签break只是跳出了内层循环（b2 b3）外层仍会循环完剩下一次（c1 c2 c3)

a1 a2 a3 b1 c1 c2 c3

使用标签标记外层循环后，直接跳出了外层循环

a1 a2 a3 b1
## 04.while循环语句
while循环先判断后执行，满足条件就进行本次循环

do..while循环先执行后判断，满足条件再进行下一次循环

```
fun main(args: Array<String>) {
    var a = -1
    while(a > 0) {
        println(a)  //不输出
        a -= 1
    }
    a = 100
    do {
        println(a)  //输出-1
        a -= 1
    }while (a > 0)
}
```
## 05.01定义range区间

```
fun main(args: Array<String>) {
    var range1 = 1..100
    var range2 = IntRange(1,100)
    var range3 = 1 until 100 //不包含100
    println(range1)  //1..100 而不是依次打印所有的数

    var longRange1 = 1L..100L
    var longRange2 = LongRange(1L,100L)
    var longRange3 = 1L until 100L //不包含100L
    println(longRange2)  //1..100

    var charRange1 = 'a'..'z'
    var charRange2 = CharRange('a','z')
    var charRange3 = 'a' until 'z' //不包含'z'
    println(charRange3)  //打印a..y
}
```
## 05.02.区间的遍历

由for循环实现，以下是四种形式

```
fun main(args: Array<String>) {
    val range = 1..10
    for(a in range) {
        println(a)
    }
    for((index, a) in range.withIndex()) {
        println("位置=$index ,数字=$a")
    }
    range.forEach {
        println(it)
    }
    range.forEachIndexed { index, a ->
        println("位置=$index ,数字=$a")
    }
}
```
## 05.03.反向区间和区间的反向

不能直接使用 10..1的定义方法 因为需要的是IntProgression型

应使用downTo定义反向区间，不可以forEach遍历

区间的反向可以使用reversed函数，区间反向后可以forEach遍历

```
fun main(args: Array<String>) {
    val range1 = 1..10
//    val range2 = 10..1 //错误的定义方法
    val range2 = 10 downTo 1 //用downTo定义反向区间
    range2.forEach {
        println(it)
    }
    val range3 = range1.reversed()
    range3.forEach {
        println(it)
    }
}
```
## 06.条件控制语句if

```
fun main(args: Array<String>) {
    val a = 10
    val b = 15

    var result = sub2(a,b)
    println("$a 和 $b 相差 $result")
    result = sub3(b,a)
    println("$b 和 $a 相差 $result")
}

fun sub(m:Int, n:Int):Int {
    if(m > n) {
        return m-n
    } else {
        return n-m
    }
}

fun sub2(m:Int, n:Int):Int {
    return if (m > n) {
        m-n
    } else {
        n-m
    }
}

fun sub3(m:Int, n:Int):Int = if (m > n) m-n else n-m
```
## 07.01.数组定义
8+1种数据类型的数组
- BooleanArray
- ByteArray
- ShortArray
- CharArray
- IntArray
- FloatArray
- DoubleArray
- LongArray
- StringArray //属于java

Any 相当于 java 中的 Object
```
fun main(args: Array<String>) {
    //自动类型推断
    val arr1 = arrayOf("张三","李四","王五")
    //Any数据类型
    val arr2 = arrayOf("张三","李四","王五",2)

    //定义一个Int类型数组
    val intArray = IntArray(10)
    val intArray0 = IntArray(10) {0}
}
```
## 07.02.数组遍历

```
fun main(args: Array<String>) {
    val arr = arrayOf("张三","李四","王五")
    for(any in arr) {
        println(any)
    }

    for((index,any) in arr.withIndex()) {
        println("index = $index any = $any")
    }

    arr.forEach {
        println(it)
    }

    arr.forEachIndexed { index, any ->
        println("index = $index any = $any")
    }
}
```

## 07.03.数组元素的修改
数组名[修改元素下标] = 新值

数组名.set(修改元素下标, 新值)
```
fun main(args: Array<String>) {
    var newArr = arrayOf(1,2,3,4,5,6)
    //第一种修改方式 - 把第1个元素改成10
    newArr[0] = 10
    newArr.forEach {
        println(it)
    }
    //第二种修改方式 - 把第2个元素改成20
    newArr.set(1,20)
    newArr.forEach {
        println(it)
    }
}
```

## 07.04.查找数组某一个元素
模板如下

```
fun main(args: Array<String>) {
    val array = arrayOf("张三","李四","王五","张三","李四","赵六")
    val index1 = array.indexOf("张三")
    println("index = $index1")
    val index2 = array.lastIndexOf("张三")
    println("last index = $index2")

    val index3 = array.indexOfFirst {
        it == "张三"
    }
    println(index3)
    val index4 = array.indexOfLast {
        it == "张三"
    }
    println(index4)
}
```
## 作业

### 1
编码实现登录功能，通过if语句判断，用户名是黑马，密码是123，表示登录成功

```
fun main(args: Array<String>) {
    var username:String?
    var password:String?
    do {
        println("输入用户名：")
        username = readLine()
        println("输入密码：")
        password = readLine()
    } while(!(username == "黑马" && password == "123"))
    println("登陆成功")
}
```

### 2
编写程序，实现输出1--100之间所有不能被7整除的数，并求和
 要求：每输出4个数据换行显示

```
fun main(args: Array<String>) {
    var sum = 0
    var flag = 0
    IntRange(1, 100).forEach {
        if(it % 7 != 0) {
            //flag != 1跳过第一次换行
            if (flag++ % 4 == 0 && flag != 1) {
               println()
            }
            print("${it} ")
            sum+=it
        }
    }
    println("\nsum=$sum")
}
```

### 3
根据用户输入数字周一到周日显示对应的英文星期名称缩写，如果用户输入的数字不是1-7的数字提示用户输入错误。

```
fun main(args: Array<String>) {
    var n = readLine()?.toInt()?:-1
    when(n) {
        1 -> println("Mon.")
        2 -> println("Tues.")
        3 -> println("Wed.")
        4 -> println("Thur.")
        5 -> println("Fri.")
        6 -> println("Sat.")
        7 -> println("Sun.")
        else -> println("输入错误")
    }
}
```

### 4
通过代码实现一周学习计划：通过用户输入今天周几，然后知道今天学习什么内容，1、3、5学习编程，2、4、6学习英语，周日休息，如果用户输入的数字不在1-7之间，提示用户输入错误。

```
fun main(args: Array<String>) {
    var n = readLine()?.toInt()?:-1
    if (n >= 1 && n < 7) {
        if(n % 2 == 0) {
            println("学习英语")
        } else {
            println("学习编程")
        }
    } else if (n == 7) {
        println("休息")
    } else {
        println("输入错误")
    }
}
```
