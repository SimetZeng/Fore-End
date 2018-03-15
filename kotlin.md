<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [概述](#概述)
- [kotlin常用操作符及用法](#kotlin常用操作符及用法)
	- [?](#)
	- [?:](#)
	- [!!](#)
	- [.. in !in](#-in-in)
	- [downTo()函数](#downto函数)
	- [step()函数](#step函数)
	- [::](#)
	- [@](#)
	- [as?](#as)
	- [is](#is)
	- [$](#)
- [数据类型](#数据类型)
	- [Boolean](#boolean)
	- [Number](#number)
	- [装箱拆箱与Char数据类型](#装箱拆箱与char数据类型)
	- [基本数据类型转换与字符串](#基本数据类型转换与字符串)
	- [类与对象](#类与对象)
	- [空类型和智能类型转换](#空类型和智能类型转换)
	- [包(Package)](#包package)
	- [区间(Range)](#区间range)
	- [数组(Array)](#数组array)
- [程序结构](#程序结构)
	- [常量与变量(val,var)](#常量与变量valvar)
	- [函数](#函数)
	- [Lambda表达式](#lambda表达式)
	- [类成员(成员方法、成员变量)](#类成员成员方法成员变量)
	- [基本运算符](#基本运算符)
	- [表达式(中缀表达式，分支表达式，when表达式等)](#表达式中缀表达式分支表达式when表达式等)
	- [循环语句(for循环、while循环、continue、break)](#循环语句for循环while循环continuebreak)
	- [异常捕获(try,catch,finally)](#异常捕获trycatchfinally)
	- [具名参数，变长参数，默认参数](#具名参数变长参数默认参数)
- [面向对象](#面向对象)
	- [面向对象-抽象类与接口](#面向对象-抽象类与接口)

<!-- /TOC -->
# 概述
Kotlin 是一个基于 JVM 的新的编程语言，由 JetBrains 开发。Kotlin已正式成为Android官方支持开发语言。

# kotlin常用操作符及用法
## ?
- 表示这个对象可能为空
  - <span style="color:red">var name: String? = "zhangsan"  </span>
  - <span style="color:red">b?.length //如果 b非空，就返回 b.length ，否则返回 null </span>

## ?:
- 如果?:左侧表达式非空，则返回其左侧表达式，反之返回右侧表达式。当且仅当左侧为空时，才会对右侧表达式求值
  - <span style="color:red">val l = b?.length ?: -1 </span>

## !!
- 返回一个非空的b值或者如果b为空就会抛出空指针异常
  - <span style="color:red">val l = b!!.length</span>

## .. in !in
- x..y：代表从x到y，包含x和y(闭区间运算符)
- until：代表从x到y，包含x但不包含y，
- in代表在一个区间中，!in代表不在一个区间中

## downTo()函数
- 倒叙遍历，区间内循环
```javascript
for (i in 4 downTo 1){
    print(i)
}
//输出4321
```

## step()函数
- 可以进行任意数量的迭代，而不是每次变化都是1
```javascript
for (i in 1..4 step 2) print(i) // prints "13"
for (i in 4 downTo 1 step 2) print(i) // prints "42"
```

## ::
- 得到类的Class对象
- <span style="color:red">startActivity(Intent(this@KotlinActivity, MainActivity::class.java))</span>

## @
- 限定this的类型
```javascript
class User {
    inner class State{
        fun getUser(): User{
            return this@User //返回User
        }
        fun getState(): State{
            return this@State //返回State
        }
    }
}
```
- 作为标签
  - 跳出多层for循环
  ```javascript
  loop@ for (itemA in arraysA) {
    var i : Int = 0
    for (itemB in arraysB) {
      i++
      if (itemB > 2) {
        break@loop
      }
      println("itemB:$itemB")
    }
  }
  ```
  - 命名函数自动定义标签
  ```javascript
  fun fun_run(){
      run {
          println("lambda")
      }
      var i: Int = run {
          return@run 1
      }
      println("$i")
      //匿名函数可以通过自定义标签进行跳转和返回
      i = run (outer@{
          return@outer 2
      })
      println(i)
  }
  ```
  - 从forEach函数跳出
  ```javascript
  fun forEach_label(ints: List<Int>) {
        var i =2
        ints.forEach {
            //forEach中无法使用continue和break;
            //if (it == 0) continue //编译错误
            //if (it == 2) break //编译错误
            print(it)
        }
         run outer@{
             ints.forEach {
                 if (it == 0) return@forEach //相当于在forEach函数中continue,实际上是从匿名函数返回
                 if (it == 2) return@outer //相当于在forEach函数中使用break,实际上是跳转到outer之外
             }
         }
        if (i == 3) {
            //每个函数的名字代表一个函数地址，所以函数自动成为标签
            return@forEach_label //等同于return
        }
    }
  ```

## as?
- 安全转型，当转型不成功时，会返回null

## is
- 判断某个实例是否是某个类型

## $
- 字符串可以包含模板表达式，及一小段代码，会求值并把结果包含到字符串中
- <span style="color:red">val value:Int=5;</span>
- <span style="color:red">val str:String="the value is $value"</span>
- <span style="color:red">var userInfo = "name:${user.name},  age:$age"</span>


# 数据类型

## Boolean
  - <span style="color:red">val aBoolean: Boolean = true</span>
  - <span style="color:red">val bBoolean: Boolean = false</span>

## Number
  - 浮点型
    - Double (64位宽)
    - Float (32)
  - 整型
    - Long (64)
    - Int (32)
    - Short (16)
  - 字节
    - Byte (8)

## 装箱拆箱与Char数据类型
- Integer(装箱类型) 与 Int(基本类型)。在kotlin中Int是Integer和Int的合体，编译器会自动识别使用哪种类型。
- Char就是Java的Character，占2个字节，表示字符，使用单引号引起
  - \t 制表符
  - \b 光标后退一个字符
  - \n 回车
  - \r 光标回到行首
  - \' 单引号
  - \" 双引号
  - \\ 反斜杠
  - \$ 美元符号,Kotlin支持美元符号开头的字符串模板

## 基本数据类型转换与字符串

## 类与对象
- 类
  - 类是一个抽象的概念
  - 具有某些特征的事物的概括
  - 不特定指代任何一个具体的事物
- 对象
  - 对象是一个具体的概念，与类相对
  - 描述某一种类的具体个体
- 类与对象的关系
  - 一个雷通常可以有很多个具体的对象
  - 一个对象本质上只能从属与一个类
  - 对象也经常被称为“类的对象”或“类的实例”
    - 城市-北京、上海、广州
    - 国家-中国、美国、德国
- 类的继承
  - 提取多个类的共性得到一个更抽象的类，即父类
  - 子类拥有父类的一切特征
  - 子类也可以自定义自己的特征
  - 所有类都最终继承自Any

## 空类型和智能类型转换
- <span style="color:red">val name: String = getName() ?: return</span>
- kotlin里用'?'判断是否为空
- 在数据类型后面加'?'表示它可为空
- 如果一个变量在定义的时候定为可空的类型，但实际这个变量却不为空，这时获取他的长度就在.之前加'!!'

## 包(Package)
- 包就是命名空间
- 包的声明必须在非注释代码的第一行
- 类的全名
  - net.println.kotlin.chapter2.HelloWorld

## 区间(Range)
- 是个数学上的概念，表示范围
- ClosedRange的子类，IntRange最常用
- 基本写法
  - 0..100 表示[0,100]
  - 0 until 100 表示[0,100)
  - i in 0..100 判断i是否在区间[0,100]中

## 数组(Array)
- 基本写法
  - <span style="color:red">val array:Array<String> = arrayOf(...)</span>
- 基本操作
  - print array[i] 输出第i个成员
  - array[i] = "Hello" 给第i个成员赋值
  - array.length 数组的长度

# 程序结构

## 常量与变量(val,var)

## 函数
- 函数就是以特定功能组织起来的代码块
  - <span style="color:red">fun [函数名] ([参数列表]): [返回值类型] {[函数体]}</span>
  - <span style="color:red">fun [函数名] ([参数列表]) = [表达式]</span>
- 例子：
  - <span style="color:red">fun sayHi (name: String) {println("Hi, $name")}</span>
  - <span style="color:red">fun sayHi (name: String) = println("Hi, $name")</span>
- 匿名函数
  - <span style="color:red">fun ([参数列表])...</span>
  - <span style="color:red">val sayHi = fun(name: String) = println("Hi, $name")</span>

## Lambda表达式
- 就是匿名函数
- 写法：{[参数列表] -> [函数体，最后一行是返回值]}
- 举例：
  - <span style="color:red">val sum = {a: Int, b: Int -> a + b}</span>
- ()->Unit
  - 无参，返回值为Unit
- (Int)->Int
  - 传入整型，返回一个整型
- (String, (String)->String)->Boolean
  - 传入字符串、Lambda表达式，返回Boolean
- 调用：用()进行调用，等价于invoke()
- 举例：
  - <span style="color:red">val sum = {a: Int,b Int -> a + b}</span>
  - <span style="color:red">sum(2,3)</span>
  - <span style="color:red">sum.invoke(2,3)</span>

## 类成员(成员方法、成员变量)
- 什么是类成员
  - 属性：或者说成员变量，类范围内的变量
  - 方法：或者说成员函数，类范围内的函数
- 函数与方法的区别
  - 函数强调功能本身，不考虑从属
  - 方法的称呼通常是从类的角度出发
  - 叫法不同而已
- 定义方法
  - <span style="color:red">class Hello {</span>
    - <span style="color:red">fun sayHello(name: String = println("Hello, $name"))</span>
  - <span style="color:red">}</span>
- 定义属性
  - 构造方法参数中val/var修饰的都是属性
  - 类内部也可以定义属性
  - <span style="color:red">class Hello(val aField:Int, notAField: Int){</span>
    - <span style="color:red">var anotherField: Float = 3f</span>
  - <span style="color:red">}</span>
- 属性访问控制
  - 属性可以定义getter/setter
  - <span style="color:red">val a:Int = 0</span>
    - <span style="color:red">get() = field</span>
  - <span style="color:red">var b: Float = 0f</span>
    - <span style="color:red">set(value) {field = value}</span>
- 属性初始化
  - 属性的初始化尽量在构造方法中完成
  - 无法在构造方法中初始化，尝试降级为局部变量
  - var用lateinit延迟初始化，val用lazy
    - <span style="color:red">ilateinit var c: String</span>
    - <span style="color:red">ival e: X by lazy {X()}</span>
  - 可控类型谨慎用null直接初始化

## 基本运算符
- 任何类可以定义或者重载父类的基本运算符
- 通过运算符对应的具体函数来定义
- 对参数个数作要求，对参数和返回值类型不作要求
- 不能像Scala一样定义任意运算符
- 一元运算符:
  | 表达式        | 转换
  | --------   | -----:
  | +a        | a.plus()
  | -a        | a.minus()
  | !a        | a.not()
  | a++       | a.inc()
  | a--       | a.dec()
- 二元运算符
  | 表达式        | 转换
  | --------   | -----:
  | a+b        | a.plus(b)
  | a-b        | a.minus(b)
  | a*b        | a.times(b)
  | a/b        | a.div(b)
  | a%b        | a.mod(b)
  | a..b       | a.rangeTo(b)


## 表达式(中缀表达式，分支表达式，when表达式等)
- if表达式
  - if...else
    - <span style="color:red">if (a == b) ... else if (a == c) ... else...</span>
  - 表达式与完备性
    - <span style="color:red">val x = if (b < 0) 0 else b</span>
    - <span style="color:red">val x = if (b < 0) 0 //错误，赋值时，分支必须完备</span>
- when表达式
  - 加强版switch，支持任意类型
  - 支持纯表达式条件分支(类似if)
  - 表达式与完备性

## 循环语句(for循环、while循环、continue、break)
- for循环
  - 基本写法
    - <span style="color:red">for (element in elements)</span>
  - 给任意类实现Iterator方法
- While循环
  - <span style="color:red">do ... while(...) ...</span>
  - <span style="color:red">while(...) ...</span>
- 跳过与终止循环
  - 跳过当前循环用continue
  - 终止循环用break
  - 多层循环嵌套的终止结合标签使用
    - <span style="color:red">Outter@for (...) {</span>
      - <span style="color:red">Inner@while(i < 0) {if (...) break@Outter}</span>
    - <span style="color:red">}</span>

## 异常捕获(try,catch,finally)
- try...catch
  - catch 分支匹配异常类型
  - 表达式，可以用来赋值
- finally
  - 无论代码是否抛异常都会执行

## 具名参数，变长参数，默认参数
- 具名参数
  - 给函数的实参附上形参
  - 例如
    - <span style="color:red">fun sum(arg1: Int, arg2: Int) = arg1 + arg2</span>
    - <span style="color:red">sum(arg1=2,arg2=3)</span>
- 变长参数
  - 某个参数可以接收多个值
  - 可以不为最后一个参数
  - 如果传参有歧义，需要使用具名参数
- 默认参数
  - 为函数参数指定默认值
  - 可以为任意位置的参数指定默认值
  - 传参时，如果有歧义，需要使用具名参数

# 面向对象

## 面向对象-抽象类与接口
- 基本概念
  - 解决如何用程序描述世界的问题
  - 如何将实际存在的东西映射成类和对象
  - 一种程序设计的思路、思想、方法
  - 程序设计层面的概念
- 抽象类与接口
