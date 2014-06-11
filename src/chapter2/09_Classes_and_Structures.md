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

The example above defines a new structure called `Resolution`, to describe a pixel-based display resolution. This structure has two stored properties called `width` and `height`. Stored properties are constants or variables that are bundled up and stored as part of the class or structure. These two properties are inferred to be of type `Int` by setting them to an initial integer value of 0.

例子定义了一个名叫`Resolution`的新结构体，用来描述一个基于像素的显示方案。这个结构体有两个~~属性~~：`宽`和`高`。~~属性~~是捆绑存储在类和结构体中的变量或常量。这两个属性的类型将被编译器推断为`Int`，并赋予初始值0。

The example above also defines a new class called `VideoMode`, to describe a specific video mode for video display. This class has four variable stored properties. The first, `resolution`, is initialized with a new `Resolution` structure instance, which infers a property type of `Resolution`. For the other three properties, new `VideoMode` instances will be initialized with an `interlaced` setting of `false` (meaning “non-interlaced video”), a playback frame rate of `0.0`, and an optional `String` value called `name`. The `name` property is automatically given a default value of `nil`, or “no `name` value”, because it is of an optional type.

例子中也定义了一个名叫`VideoMode`的新类,用来表示视频显示的模式。VideoMode类中有四个属性。第一个是`resolution`，它在这里被初始化为一个新的`Resolution`结构体实例，而编译器将自动推断分辨率的类型为`Resolution`。除此之外新的`VideoMode`实例还将初始化三个属性，默认为`false`的`interlaced`（意味着这是个“不交错的视频”），默认值为`0.0`表示播放帧速率的`frameRate`，以及一个值可选类型为`String`的`name`。属性`name`将自动赋值为`nil`，或者说`name`无值，因为它的值是可选的。

### Class and Structure Instances
### 类和结构体的实例

The `Resolution` structure definition and the `VideoMode` class definition only describe what a `Resolution` or `VideoMode` will look like. They themselves do not describe a specific resolution or video mode. To do that, you need to create an instance of the structure or class.

结构体`Resolution`和类`VideoMode`的定义只是告诉你`Resolution`和`VideoMode`含有什么内容。但他们本身并不描述一个特定的分辨率或者视频模式。要做到这一点，我们要生成一个他们的实例。

The syntax for creating instances is very similar for both structures and classes:

生成结构体实例和生成类实例的语法非常类似：

```
let someResolution = Resolution()
let someVideoMode = VideoMode()
```

Structures and classes both use initializer syntax for new instances. The simplest form of initializer syntax uses the type name of the class or structure followed by empty parentheses, such as `Resolution()` or `VideoMode()`. This creates a new instance of the class or structure, with any properties initialized to their default values. Class and structure initialization is described in more detail in [Initialization]().

结构体和类都是用初始化语法来生成新的实例。初始化语法最简单的形式是结构体或类的类型名后加上空括号，例如`Resolution()`和`VideoMode()`。这将创建一个所有的属性都是默认值的结构体或类。类和结构体的初始化在[构造过程]()章节中有更详细的说明。

### Accessing Properties
### 属性的访问
You can access the properties of an instance using *dot syntax*. In dot syntax, you write the property name immediately after the instance name, separated by a period (.), without any spaces:

你可以使用*点语法*访问实例的属性。使用点语法时，属性名将紧跟在实例名之后，中间以句号（.）隔开：

```
println("The width of someResolution is \(someResolution.width)")
// prints "The width of someResolution is 0
```

In this example, `someResolution.width` refers to the `width` property of `someResolution`, and returns its default initial value of `0`.

在这个例子中，`someResolution.width`表示`someResolution`的`width`属性，且返回默认初始值`0`。

You can drill down into sub-properties, such as the `width` property in the `resolution` property of a `VideoMode`:

你可以继续使用点语法来访问属性的属性，例如`VideoMode`中`resolution`的属性`width`:

```
println("The width of someVideoMode is \(someVideoMode.resolution.width)")
// prints "The width of someVideoMode is 0"
```

You can also use dot syntax to assign a new value to a variable property:
我们还可以使用点语法来为属性变量赋值：

```
someVideoMode.resolution.width = 1280
println("The width of someVideoMode is now \(someVideoMode.resolution.width)")
// prints "The width of someVideoMode is now 1280"
```

```
NOTE

Unlike Objective-C, Swift enables you to set sub-properties of a structure property directly. In the last example above, the width property of the resolution property of someVideoMode is set directly, without your needing to set the entire resolution property to a new value.
```
```
注意：

与Objective-C不同，Swift允许直接为结构体的属性的子属性赋值。在上方的例子中，someVideoMode中属性resolution的子属性width被直接赋值了，不再需要给整个resolution属性赋予新值。
```
‌
### Memberwise Initializers for Structure Types
### 结构体带参数的初始化方法

All structures have an automatically-generated memberwise initializer, which you can use to initialize the member properties of new structure instances. Initial values for the properties of the new instance can be passed to the memberwise initializer by name:

所有结构体都有一个自动生成的带参数的初始化方法，用于新结构体实例成员属性的初始化。新实例属性的初值会通过变量名传递到带参数的初始化方法里：

```
let vga = Resolution(width: 640, height: 480)
```

Unlike structures, class instances do not receive a default memberwise initializer. Initializers are described in more detail in [Initialization]().
与结构体不同，类市里没有默认的带参数的初始化方法。对初始化方法的详细说明见[构造过程]()章节。

‌
### Structures and Enumerations Are Value Types
### 结构体和枚举都是值类型

A value *type* is a type that is copied when it is assigned to a variable or constant, or when it is passed to a function.
值*类型*的变量在赋值给一个变量、常量或作为参数传给函数时，传递的是该变量值的拷贝。

You’ve actually been using value types extensively throughout the previous chapters. In fact, all of the basic types in Swift—integers, floating-point numbers, Booleans, strings, arrays and dictionaries—are value types, and are implemented as structures behind the scenes.

All structures and enumerations are value types in Swift. This means that any structure and enumeration instances you create—and any value types they have as properties—are always copied when they are passed around in your code.

Consider this example, which uses the Resolution structure from the previous example:

let hd = Resolution(width: 1920, height: 1080)
var cinema = hd
