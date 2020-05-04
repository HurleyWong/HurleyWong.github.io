---
title: Kotlin基础（一）
tags:
  - Kotlin基础
categories: 
  - Kotlin
date: 2020-01-12
---

## Hello World

```kotlin
fun main(args: Array<String>) {
  println("Hello World")
}
```

`fun main(args: Array<String>)`也可以直接写成`fun main()`。

<!-- more -->

## 变量

### 变量声明

在Kotlin中，使用关键字`var`和`val`声明变量。

```kotlin
var language = "Kotlin"
val salary = 10000
```

Kotlin中不需要明确指定变量的类型。Kotlin编译器通过`initilizer`表达式自动识别推断变量的类型。当然，在声明变量时也可以明确指定变量的类型。

```kotlin
var language: String = "Kotlin"
val salary: Int = 10000
```

### 关键字var和val的区别

* val用来定义常量，即恒定不变的量。

```kotlin
val constant = 1
```

* var定义变量，即可变动的量。

```kotlin
var variable = 5
```

#### 如何分清

如果不清楚什么时候使用常量什么时候使用变量时，可以优先使用常量val，如果IDE提示错误则改为var。

当使用val定义为常量时，常量是不能变动的，只能为其赋值一次。所以如果要改变它的值，需要使用var改成变量。

```
var str: String = "abc" => public String str = "abc"
val str: String = "abc" => public final String str = "abc"
```

#### 进阶

实际上，val表示的是**只读（read-only）**，即不能再将值写入val，并不意味着其是不可变的。

在Kotlin的类中，val和var用于表示属性是否有getter/setter：

* var：同时有getter和setter
* val：只有getter

### lateinit和lazy

如果不想在一开始就对一个属性进行初始化，那么可以使用以下两个关键字。

* lateinit
* lazy

#### lateint

通常情况下，声明为非null类型的属性必须初始化，可以使用`lateinit`修饰符修饰属性。

```kotlin
lateinit var user: User
```

* `lateinit`只能用于`var`声明的类变量，并且属性没有自定义`getter`和`setter`方法
* 属性的类型必须是非空的，并且不能是原始类型

#### lazy

`lazy()`是一个函数，它接收一个`lambda`并返回一个`lazy`实例，它可以作为一个实现`lazy`属性的委托。

```kotlin
val name: String by lazy {"Android Developer"}
```

#### 对比

* `lazy`只能用于`val`属性，而`lateinit`只能用于`var`属性
* `lateinit var`可以从任何能看到对象的地方进行初始化。如果想要属性在外部被初始化，可以使用`lateinit`

## 数据类型

* 数字类型
* 字符类型
* 布尔类型
* 数组类型
* 字符串类型

### 数字类型

分为整数和浮点数。

* Byte
* Short
* Int
* Long
* Float
* Double

### 字符类型(Char)

使用关键字`char`表示，使用单引号`''`声明。

### 布尔数据类型(Boolean)

使用关键字`Boolean`表示，包含`true`和`false`。

### 数组类型

Kotlin中的数组用`Array`表示。使用库函数`arrayOf()`和`Array()`构造函数创建数组。`Array`中有`get()`、`set()`函数，`size`属性等。

#### 使用`arrayOf`创建数组

例如`arrayOf(1,2,3)`，它创建一个数组`[1,2,3]`。通过索引值`array[index]`访问数组的元素，索引从0开始。

#### 使用`Array()`创建数组

使用`Array()`构造函数创建数组时，需要在`Array()`构造函数中使用两个参数：

* 第一个参数作为数组的大小
* 第二个参数作为函数，用于初始化并返回给定索引的数组元素的值

```kotlin
val asc = Array(5, {i -> i * 2}) // asc[0,2,4,6,8]
```

### 字符串类型

使用`String`表示。

## 类型转换

* `toByte()`
* `toShort()`
* `toInt()`
* `toLong()`
* `toFloat()`
* `toDouble()`
* `toChar()`

## When表达式

Kotlin中的`when`表达式相当于`switch`语句。

```kotlin
fun main(args: Array<String>) {
  var number = 4
  var numberProvided = when(number) {
    1 -> "One"
    2 -> "Two"
    3 -> "Three"
    4 -> "Four"
    else -> "invalid number"
  }
  println("You provide $numberProvided")
}
```

## For循环

```kotlin
for (item in collection) {  
}
for (i in 1..5) {
}
for (i in 1 until 5) {
}
```







