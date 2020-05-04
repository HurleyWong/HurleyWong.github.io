---
title: Kotlin基础（二）
tags:
  - Kotlin基础
categories: 
  - Kotlin
date: 2020-01-13
---

## 可空和非可空类型

在Kotlin中，对于`null`安全类型是一种消除代码中空引用风险的过程。如果Kotlin编译器发现任何`null`参数而仍然执行`null`引用相关语句，则会立即抛出`NullPointerException`。

Kotlin类型系统区分可以保持`null`（可空引用）和不能保持`null`（非`null`引用）的引用。通常，`String`类型是不可为`null`的。要创建保存`null`值的字符串，必须要放置一个`?`来明确定义。例如，`String?`

### 可空类型

通过放置一个`?`来声明可空类型`?`在String后面

<!-- more -->

```kotlin
var str1: String? = "hello"
str1 = null	// ok
```

这时候`str1`可以等于`null`。

### 非可空类型

非可空类型是普通字符串，它们声明为`String`类型

```kotlin
val str: String = null	// compile error
str = "hello"	// compile error Val cannot be reassign
var str2: String = "hello"
str2 = null	// compile error
```

第一行的错误是没有将`str`定义为可空类型就令它为`null`。第二行的错误是使用`val`定义`str`，那么之后`str`的值是不可更改的。第三、四行虽然用`var`定义`str2`，但是同样没有定义为可空类型，所以不可令`str2 = null`。

## 智能类型转换

在没有安全转换的情况下访问可空类型的`String`时，它将生成编译错误。例如：

```kotlin
var string: String? = "Hello"
print(string.length)	//compile error
```

如上代码会报错，因为没有判断字符串是否为空。

而使用安全转换为：

```kotlin
fun main() {
  var string: String? = "Hello"
  if (string != null) {
    print(string.length)
  }
}
```

在判断string不为空后，就可以正常执行。

### 使用is或!is来智能转换

```kotlin
fun main() {
  val obj: Any = "Hello"
  if (obj is String) {
    println("字符串长度：${obj.length}")
  }
}
```

## 不安全和安全类型转换

### 不安全转换操作符：as

有时无法转换变量并抛出异常，这称为不安全转换。例如，可以为空的字符串`String?`不能转换成非null字符串`String`，这会造成异常。

```kotlin
fun main() {
  val obj: Any? = null
  val str: String = obj as String
  println(str)
}
```

上述代码把`Any`类型转换为字符串类型会造成`ClassCastException`异常。

### 安全转换操作符：as?

Kotlin提供一种安全转换操作符：`as?`。如果无法进行转换，则返回`null`，而不是抛出异常。例如：

```kotlin
fun main() {
  val location: Any = "Kotlin"
  val safeString: String? = location as? String
  val safeInt: Int? = location as? Int
  println(safeString)
  println(safeInt)
}
```

执行代码得到的结果：

```
Kotlin
null
```

因为`Any`类型的`Kotlin`可以转换成`String`类型但是不能转换成`Int`类型，所以第二个输入为`null`。

## Elvis运算符

Elvis运算符用来返回非`null`值，即使条件表达式为`null`。可以用来**检查值的空安全性**。

假设一个包含空引用的变量`str`，在程序中使用`str`之前要检查它的可空性。如果发现变量`str`不为`null`，则其属性可以使用，否则就得返回其它非空值。**（总之不能返回`null`）**。

Kotlin还提供称为Elvis运算符(`?:`)的高级运算符，即使条件表达式为空，也返回非空值。

### 使用方法

```kotlin
var str: String? = null
var str2: String? = "nullable string"
var len1: Int = str?.length ?: -1
var len2: Int = str2?.length ?: -1
```

通过Elvis运算符就相当于使用传统的`if...else`语句执行此安全检查。

上述代码通过判断`str`是否为空，如果为空，就返回正常的`str.length`，否则返回`?:`后的值-1。

除此之外，Elvis运算符后还可以使用`throw`和`return`表达式。

```kotlin
var text1 = text1 ?: return null
var text2 = text2 ?: IllegalArgumentException("text exception")
```

## 静态属性和静态方法

Kotlin类不支持静态方法和成员，但是Kotlin支持全局函数和变量，所以可以直接使用全局函数和变量来代替类中静态方法和静态成员变量。

Kotlin中有一个有趣的语法糖：`Objects`。它可以解决由于没有`static`而造成的麻烦。

### 静态类

指类中所有的方法都为静态方法的情况，例如工具类一般是静态类。

**把类名`class`改成`object`即可**

```kotlin
object DateUtil {
    // 静态方法
}
```

### 静态方法

这里又要引入Kotlin另一个语法糖：`Companion Objects`。在类的内部可以用`companion object{}`包裹所需的静态方法

```kotlin
companion object {
    private const val TAG = "LoginActivity"
}
```

`companion object`中定义的成员变量就可以通过类名直接访问。











