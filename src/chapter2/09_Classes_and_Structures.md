## Classes and Structures
## 类与结构体

*Classes* and *structures* are general-purpose, flexible constructs that become the building blocks of your program’s code. You define properties and methods to add functionality to your classes and structures by using exactly the same syntax as for constants, variables, and functions.”  

*类*和*结构体*是通用的、灵活的结构，是您搭建代码的基石。您可以使用和定义常量、变量或函数相同的句法，为类添加属性和方法以增加新的功能。  

Unlike other programming languages, Swift does not require you to create separate interface and implementation files for custom classes and structures. In Swift, you define a class or a structure in a single file, and the external interface to that class or structure is automatically made available for other code to use.

与其他编程语言不同，Swift并不强制要求分隔自定义类或结构体的头文件和实现文件。在Swift中，你只需将类或结构体定义在一个文件中，这个类或结构体的外部接口就自动能被其他代码使用。

```
NOTE

An instance of a class is traditionally known as an object. However, Swift classes and structures are much closer in functionality than in other languages, and much of this chapter describes functionality that can apply to instances of either a class or a structure type. Because of this, the more general term instance is used.
```

```
注意
类的实例通常被当作为一个对象。但与其他语言相比，Swift中的类和结构体从功能上来说更为相似。本章中介绍的大部分功能，可以适用于任何一个类或者结构体的实例。因此我们将使用一个更加宽泛的词语--实例(instance)来描述类和结构体。
```

### Comparing Classes and Structures
### 比较类和结构体
Classes and structures in Swift have many things in common. Both can:

* Define properties to store values
* Define methods to provide functionality
* Define subscripts to provide access to their values using subscript syntax
* Define initializers to set up their initial state
* Be extended to expand their functionality beyond a default implementation
* Conform to protocols to provide standard functionality of a certain kind

For more information, see [Properties](), [Methods](), [Subscripts](), [Initialization](), [Extensions](), and [Protocols]().


在Swift中类和结构体有许多相同之处，它们都有如下功能：

* 能定义属性以便存储数据
* 能定义方法以便提供功能
* ~~定义了下标以便使用下标语法来访问实例的值~~
* 能定义设定初始状态的初始化方法
* 能被扩展，使其有默认实现之外的功能
* 遵从协议(protocol)规则，以便提供~~协议所规定类型的标准功能~~

欲了解更多信息，请参见[属性]()，[方法]()，[下标]()，[构造过程]()，[扩展]()和[协议]()章节。

Classes have additional capabilities that structures do not:

* Inheritance enables one class to inherit the characteristics of another.
* Type casting enables you to check and interpret the type of a class instance at runtime.
* Deinitializers enable an instance of a class to free up any resources it has assigned.
* Reference counting allows more than one reference to a class instance.

For more information, see [Inheritance](), [Type Casting](), [Initialization](), and [Automatic Reference Counting]().

不过类也有一些结构体没有的额外功能：

* 继承使得一个类能继承来自另一个类的特性。
* 类型转换可以在运行时检查和解析一个类的实例的类型。
* 析构方法让类的实例被~~指派给了其他内存~~时能够释放自己的资源。
* 引用计数允许一个类的实例被多处引用。

欲了解更多信息，请参见[继承](),[类型转换]()，[构造过程]()，[自动引用计数]()章节。

```
NOTE

Structures are always copied when they are passed around in your code, and do not use reference counting.
```

```
注意：
结构体在代码中被传递时始终是传值，不会涉及到引用计数

```

‌
### Definition Syntax
### 定义语法

Classes and structures have a similar definition syntax. You introduce classes with the `class` keyword and structures with the `struct` keyword. Both place their entire definition within a pair of braces:

定义类和结构体的语法相似。定义类以关键词`class`开头，而定义结构体以关键词`struct`开头。类和结构体的所有定义都写在一对大括号内：

```
class SomeClass {
    // class definition goes here
}
struct SomeStructure {
    // structure definition goes here
}
```



```
NOTE

Whenever you define a new class or structure, you effectively define a brand new Swift type. Give types UpperCamelCase names (such as SomeClass and SomeStructure here) to match the capitalization of standard Swift types (such as String, Int, and Bool). Conversely, always give properties and methods lowerCamelCase names (such as frameRate and incrementCount) to differentiate them from type names.
```


```
注意：

当你定义一个新的类或者结构体时，你实际上定义了一种新的Swift类型。为了和Swift标准类型(像String，Int，Bool)保持一致，请使用首字母大写的驼峰命名法（例如SomeClass或者SomeStructure）。相反的，为了和类型名区分，属性和方法名建议使用小写驼峰命名法（如frameRate或者incrementCount）。
```

Here’s an example of a structure definition and a class definition:

下方给出了结构体和类定义的例子：


```
struct Resolution {
    var width = 0
    var height = 0
}
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
```

The example above defines a new structure called Resolution, to describe a pixel-based display resolution. This structure has two stored properties called width and height. Stored properties are constants or variables that are bundled up and stored as part of the class or structure. These two properties are inferred to be of type Int by setting them to an initial integer value of 0.

以上例子定义了一个叫Resolution的结构体，用来描述一个基于像素的显示方案。这个结构体有两个属性：宽和高。