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

实际上在前面章节我们已经广泛使用了值类型。事实上Swift中几乎所有的基本类型---如整数、浮点数、布尔值、字符串、数组和字典，都是值类型，并在底层都以结构体的方式来实现。

All structures and enumerations are value types in Swift. This means that any structure and enumeration instances you create—and any value types they have as properties—are always copied when they are passed around in your code.

Swift中的所有结构体和枚举都是值类型。这意味着你创建的任何一个结构体或枚举的实例，以及他们的属性在代码中被传递的时候都会被复制。

Consider this example, which uses the `Resolution` structure from the previous example:

让我们来看看这个例子，它使用了先前例子中定义的`Resolution`:

```
let hd = Resolution(width: 1920, height: 1080)
var cinema = hd
```

This example declares a constant called `hd` and sets it to a `Resolution` instance initialized with the width and height of full HD video (`1920` pixels wide by `1080` pixels high).

例子中声明了一个名叫`hd`的常量，并将它初始化为全高清视频分辨率（宽`1920`长`1080`）的`Resolution`实例。

It then declares a variable called `cinema` and sets it to the current value of `hd`. Because `Resolution` is a structure, a copy of the existing instance is made, and this new copy is assigned to `cinema`. Even though `hd` and `cinema` now have the same width and height, they are two completely different instances behind the scenes.
然后例子中声明了一个变量`cinema`，将`hd`的当前值赋给了它。由于`Resolution`是结构体，赋值操作会生成一个新的实例并传递给`cinema`。因此虽然`hd`和`cinema`有相同的宽高，但它们实际上仍是完全不同的实例。

Next, the `width` property of `cinema` is amended to be the width of the slightly-wider 2K standard used for digital cinema projection (`2048` pixels wide and `1080` pixels high):

接下来，将`cinema`的`width`属性改为数字电影中2K宽屏的标准宽度（宽`2048`像素高`1080`像素）：

```
cinema.width = 2048
```

Checking the `width` property of `cinema` shows that it has indeed changed to be `2048`:

检查一下`cinema`的`width`属性的确改成了`2048`：

```
println("cinema is now \(cinema.width) pixels wide")
// prints "cinema is now 2048 pixels wide"
```

However, the `width` property of the original `hd` instance still has the old value of `1920`:
不过，原来的`hd`实例的`width`属性还是旧值`1920`：

```
println("hd is still \(hd.width) pixels wide")
// prints "hd is still 1920 pixels wide"
```

When `cinema` was given the current value of `hd`, the *values* stored in `hd` were copied into the new `cinema` instance. The end result is two completely separate instances, which just happened to contain the same numeric values. Because they are separate instances, setting the width of `cinema` to `2048` doesn’t affect the width stored in `hd`.

当使用`hd`给`cinema`赋值时，`hd`存储的*值*被复制了一份并传递给`cinema`实例。结果`hd`和`cinema`成为了仅仅是属性值相同的两个完全无关的实例。所以将`cinema`的`width`属性改为`2048`不会影响`hd`中的`width`值。

The same behavior applies to enumerations:
枚举也有相同的特性：

```
enum CompassPoint {
    case North, South, East, West
}
var currentDirection = CompassPoint.West
let rememberedDirection = currentDirection
currentDirection = .East
if rememberedDirection == .West {
    println("The remembered direction is still .West")
}
// prints "The remembered direction is still .West"
```

When `rememberedDirection` is assigned the value of `currentDirection`, it is actually set to a copy of that value.

当`rememberedDirection`赋值为`currentDirection`时，实际上只是赋值了值拷贝而已。

Changing the value of `currentDirection` thereafter does not affect the copy of the original value that was stored in `rememberedDirection`.
改变`currentDirection`的值并不会影响存储了原始值副本的`rememberedDirection`。
‌
### Classes Are Reference Types
### 类是引用类型

Unlike value types, *reference types* are not copied when they are assigned to a variable or constant, or when they are passed to a function. Rather than a copy, a reference to the same existing instance is used instead.

与值类型不同，在赋值给变量、常量或者传参时，引用类型不会被复制，而是传递与当前值相同的引用。

Here’s an example, using the `VideoMode` class defined above:
请看这个例子，例子中使用了上文定义的`VideoMode`：

```
let tenEighty = VideoMode()
tenEighty.resolution = hd
tenEighty.interlaced = true
tenEighty.name = "1080i"
tenEighty.frameRate = 25.0
```

This example declares a new constant called `tenEighty` and sets it to refer to a new instance of the `VideoMode` class. The video mode is assigned a copy of the HD resolution of `1920` by `1080` from before. It is set to be interlaced, and is given a name of `"1080i"`. Finally, it is set to a frame rate of `25.0` frames per second.

例子中声明了一个名为`tenEighty`的新常量，并将它赋值为一个新的`VideoMode`实例。视频模式使用了上文的`hd`值的拷贝，其分辨率为`1920`x`1080`。`tenEighty`的`interlaced`为true，`name`为`1080i`，`frameRate`为`25.0`帧每秒。

Next, `tenEighty` is assigned to a new constant, called `alsoTenEighty`, and the frame rate of `alsoTenEighty` is modified:

然后，一个新常量`alsoTenEighty`被赋值为`tenEighty`，`alsoTenEighty`的帧率做了如下修改：

```
let alsoTenEighty = tenEighty
alsoTenEighty.frameRate = 30.0
```

Because classes are reference types, `tenEighty` and `alsoTenEighty` actually both refer to the same `VideoMode` instance. Effectively, they are just two different names for the same single instance.

因为类是引用类型，`tenEighty`和`alsoTenEighty`都指向了同一个`VideoMode`实例。实际上它们是同一个实例的两个不同的名字而已。

Checking the `frameRate` property of `tenEighty` shows that it correctly reports the new frame rate of `30.0` from the underlying `VideoMode` instance:

接下来我们检查一下`tenEighty`的属性`frameRate`，这能说明`VideoMode`实例的帧率真的变成了新值`30.0`。

```
println("The frameRate property of tenEighty is now \(tenEighty.frameRate)")
// prints "The frameRate property of tenEighty is now 30.0"
```

Note that `tenEighty` and `alsoTenEighty` are declared as constants, rather than variables. However, you can still change `tenEighty.frameRate` and `alsoTenEighty.frameRate` because the values of the `tenEighty` and `alsoTenEighty` constants themselves do not actually change. `tenEighty` and `alsoTenEighty` themselves do not “store” the `VideoMode` instance—instead, they both refer to a `VideoMode` instance behind the scenes. It is the `frameRate` property of the underlying `VideoMode` that is changed, not the values of the constant references to that `VideoMode`.

请注意`tenEighty`和`alsoTenEighty`都被声明成了常量而不是变量。但是因为修改其属性的值并不会改变`tenEighty`和`alsoTenEighty`的值，我们还是可以修改`tenEighty.frameRate`和`alsoTenEighty.frameRate`。`tenEighty`和`alsoTenEighty`并不存储`VideoMode`实例，而是引用一个`VideoMode`实例的地址。改变`frameRate`的值只是改变了引用的`VideoMode`实例的属性，并没有改变引用的`VideoMode`的地址。
‌
### Identity Operators
### 身份操作符

Because classes are reference types, it is possible for multiple constants and variables to refer to the same single instance of a class behind the scenes. (The same is not true for structures and enumerations, because they are value types and are always copied when they are assigned to a constant or variable, or passed to a function.)

因为类是引用类型，因此允许多个常量和变量都引用同一个类实例。（结构体和枚举却不是，因为它们是值类型，并且在赋值给变量常量或者传值的时候传递的都是值的拷贝。）

It can sometimes be useful to find out if two constants or variables refer to exactly the same instance of a class. To enable this, Swift provides two identity operators:

* Identical to (===)
* Not identical to (!==)

有时候需要判断两个常量或变量是否指向同一个类实例。Swift提供了两个身份操作符来实现这个功能：

 * 指向同一实例(===)
 * 指向不同实例（!==）

Use these operators to check whether two constants or variables refer to the same single instance:

以下例子使用了这两个操作符来判断两个常量或变量是否是同一实例：

```
if tenEighty === alsoTenEighty {
    println("tenEighty and alsoTenEighty refer to the same Resolution instance.")
}
// prints "tenEighty and alsoTenEighty refer to the same Resolution instance."
```

Note that “identical to” (represented by three equals signs, or ===) does not mean the same thing as “equal to” (represented by two equals signs, or ==):

提示：三个等号(===)的身份相等与两个等号(==)的值相等操作符是不一样的。

* “Identical to” means that two constants or variables of class type refer to exactly the same class instance.
* “Equal to” means that two instances are considered “equal” or “equivalent” in value, for some appropriate meaning of “equal”, as defined by the type’s designer.

 * 身份相等操作符两端的变量或常量比较的是是否从同一个类实例化而来。
 * 值相等操作符比较的则是两端的值或者对象的内存地址是否相等，这更接近我们平常理解的相等比较。

When you define your own custom classes and structures, it is your responsibility to decide what qualifies as two instances being “equal”. The process of defining your own implementations of the “equal to” and “not equal to” operators is described in Equivalence Operators.

每当你定义一个类或者结构体时，你就有义务对两个实例的“相等”标准作出决断。在[比较运算符](#)中会描述如何去对对相等和不等的比较进行实现。
‌
### Pointers
### 指针

If you have experience with C, C++, or Objective-C, you may know that these languages use pointers to refer to addresses in memory. A Swift constant or variable that refers to an instance of some reference type is similar to a pointer in C, but is not a direct pointer to an address in memory, and does not require you to write an asterisk (*) to indicate that you are creating a reference. Instead, these references are defined like any other constant or variable in Swift.

如果你之前有过编写C、C++或者Objective-C的经验，你应该会知道这些语言的指针都是对一个内存中的地址做引用的。一个变量或常量在Swift中与C的指针类似引用一个可以被引用的实例，但它不直接指向内存的某一个地址，也不需要在申明引用的变量名前加上星号(*)。在Swift中除此之外，引用的定义与其他语言相同。

## Choosing Between Classes and Structures

You can use both classes and structures to define custom data types to use as the building blocks of your program’s code.

在定义时你可以在你的代码中同时使用类和结构体来表示合适的数据类型。

However, structure instances are always passed by value, and class instances are always passed by reference. This means that they are suited to different kinds of tasks. As you consider the data constructs and functionality that you need for a project, decide whether each data construct should be defined as a class or as a structure.

他们拥有不同的特性，结构体实例被赋值时始终传递的是值的拷贝，而类实例则始终传递的是引用。将他们根据项目的实际情况去选择定义出合适的数据是代码构建者应该去仔细斟酌的。

As a general guideline, consider creating a structure when one or more of these conditions apply:

通常来说，符合以下一个或多个条件时应该使用结构体去定义数据：

* The structure’s primary purpose is to encapsulate a few relatively simple data values.
* It is reasonable to expect that the encapsulated values will be copied rather than referenced when you assign or pass around an instance of that structure.
* Any properties stored by the structure are themselves value types, which would also be expected to be copied rather than referenced.
* The structure does not need to inherit properties or behavior from another existing type.

* 结构体主要目的时用来将少量相关数据进行封装。
* 当期望实例在赋值时传递的是封装的值的被拷贝而不是仅仅是引用。
* 当期望数据结构中的只类型也一同拷贝传值而不是传递引用。
* 这个数据结构不需要去继承别的类。

Examples of good candidates for structures include:

适合使用结构体的场景：

* The size of a geometric shape, perhaps encapsulating a width property and a height property, both of type Double.
* A way to refer to ranges within a series, perhaps encapsulating a start property and a length property, both of type Int.
* A point in a 3D coordinate system, perhaps encapsulating x, y and z properties, each of type Double.

In all other cases, define a class, and create instances of that class to be managed and passed by reference. In practice, this means that most custom data constructs should be classes, not structures.

* 用来描述几何图形的尺寸，包含了浮点类型的宽和高两个属性。
* 用来描述一个范围，包含一个整型开始值和一个整型长度。
* 用来描述一个三维坐标系统，包含双精度的x,y和z三个属性。

所有其他情况请定义类并使用类的实例以引用方式传递。实际上大多数情况还是应该用类来作为主要的数据结构承载，结构体仅在必要时。

## Assignment and Copy Behavior for Collection Types

## 集合的赋值与拷贝

Swift’s Array and Dictionary types are implemented as structures. However, arrays have slightly different copying behavior from dictionaries and other structures when they are assigned to a constant or variable, and when they are passed to a function or method.

在Swift中Array和Dictionary类型都是使用结构体实现的。然而当Array被赋值给常量、变量或者当作参数传入一个方法或者函数中时拷贝操作与Dictionary和其他结构体略有不同。

The behavior described for Array and Dictionary below is different again from the behavior of NSArray and NSDictionary in Foundation, which are implemented as classes, not structures. NSArray and NSDictionary instances are always assigned and passed around as a reference to an existing instance, rather than as a copy.

以下Array和Dictionary与Foundation框架中的NSArray和NSDictionary的实现方式是有去别的，后者使用类实现，其实例在传递过程中均以引用形式进行传递而不是拷贝。

> NOTE
> 
> The descriptions below refer to the “copying” of arrays, dictionaries, strings, and other values. Where copying is mentioned, the behavior you see in your code will always be as if a copy took place. However, Swift only performs an actual copy behind the scenes when it is absolutely necessary to do so. Swift manages all value copying to ensure optimal performance, and you should not avoid assignment to try to preempt this optimization.

> 提示
>
> 以下是对于数组，字典，字符串和其它值的拷贝的描述。 在你的代码中出现拷贝引用的地方便会一直时拷贝引用。然而，Swift只在确实有必要发生拷贝行为的场景下才回执行拷贝操作。为了性能的最优，Swift将会在最合适的实际进行拷贝操作，以达到性能最优的目的，而开发者不关心这方面的性能问题也没关系。

### Assignment and Copy Behavior for Dictionaries

### Dictionary的赋值与拷贝

Whenever you assign a Dictionary instance to a constant or variable, or pass a Dictionary instance as an argument to a function or method call, the dictionary is copied at the point that the assignment or call takes place. This process is described in Structures and Enumerations Are Value Types.

只要将一个字典实例进行赋值或者传参操作，就会产生拷贝行为，在[结构体和枚举都是值类型](#)小节中有详细描述过。

If the keys and/or values stored in the Dictionary instance are value types (structures or enumerations), they too are copied when the assignment or call takes place. Conversely, if the keys and/or values are reference types (classes or functions), the references are copied, but not the class instances or functions that they refer to. This copy behavior for a dictionary’s keys and values is the same as the copy behavior for a structure’s stored properties when the structure is copied.

如果字典实例中所储存的键值是结构体或枚举类型，那么赋值的时候也是拷贝赋值。相反，如果键值是引用类型，那么赋值操作只传递会引用，而不是实例本身的拷贝。在结构体中的键值也具有相同特性。

The example below defines a dictionary called ages, which stores the names and ages of four people. The ages dictionary is then assigned to a new variable called copiedAges and is copied when this assignment takes place. After the assignment, ages and copiedAges are two separate dictionaries.

下面的示例定义了一个名为ages的字典实例，存储了四个人的名字和年龄。ages被赋值给了一个名为copiedAges的新变量时字典实例被重新复制了一份。赋值结束后，ages和copiedAges成为两个相互独立的字典实例。

```
var ages = ["Peter": 23, "Wei": 35, "Anish": 65, "Katya": 19]
var copiedAges = ages
```

The keys for this dictionary are of type String, and the values are of type Int. Both types are value types in Swift, and so the keys and values are also copied when the dictionary copy takes place.

这个字典的键是字符串型，值是整型。这两种类型在Swift 中都是值类型，所以当字典被拷贝时，它们也都会被一起拷贝。

You can prove that the ages dictionary has been copied by changing an age value in one of the dictionaries and checking the corresponding value in the other. If you set the value for "Peter" in the copiedAges dictionary to 24, the ages dictionary still returns the old value of 23 from before the copy took place:

我们可以通过改变一个字典中的年龄，然后检查另一个字典中所对应的值，来证明ages字典确实是被拷贝了。如果在copiedAges字典中将Peter的值设为24，那么ages字典中Peter值仍然会返回23：

```
copiedAges["Peter"] = 24
println(ages["Peter"])
// prints "23"
```

### Assignment and Copy Behavior for Arrays
### 数组的赋值与拷贝

The assignment and copy behavior for Swift’s Array type is more complex than for its Dictionary type. Array provides C-like performance when you work with an array’s contents and copies an array’s contents only when copying is necessary.

在Swift 中，数组(Arrays)类型的赋值和拷贝行为要比字典(Dictionary)类型的复杂的多。当操作数组内容时，数组(Array)能提供接近C语言的的性能，并且拷贝行为只有在必要时才会发生。

If you assign an Array instance to a constant or variable, or pass an Array instance as an argument to a function or method call, the contents of the array are not copied at the point that the assignment or call takes place. Instead, both arrays share the same sequence of element values. When you modify an element value through one array, the result is observable through the other.

如果你将一个数组(Arrays)实例赋给一个变量或常量，或者将其作为参数传递给函数或方法，在事件发生时数组的内容不会被拷贝。而且两个数组使用的还是同一套序列。只有当你在一个数组内修改某一元素，修改结果才c会在另一数组显示。

For arrays, copying only takes place when you perform an action that has the potential to modify the length of the array. This includes appending, inserting, or removing items, or using a ranged subscript to replace a range of items in the array. If and when array copying does take place, the copy behavior for an array’s contents is the same as for a dictionary’s keys and values, as described in Assignment and Copy Behavior for Dictionaries.

对数组来说，拷贝行为仅仅当操作有可能修改数组长度时才会发生。这种行为包括了附加(appending),插入(inserting),删除(removing)或者使用范围下标(ranged subscript)去替换这一范围内的元素。只有当数组拷贝确要发生时，数组内容的行为规则与字典中键值的相同，详见[Dictionary的赋值与拷贝](#)。

The example below assigns a new array of Int values to a variable called a. This array is also assigned to two further variables called b and c:

下面的示例将一个整数数组赋给了一个名为a的变量，继而又被赋给了变量b和c：

```
var a = [1, 2, 3]
var b = a
var c = a
```

You can retrieve the first value in the array with subscript syntax on either a, b, or c:

我们可以在a,b,c上使用下标语法以得到数组的第一个元素：

```
println(a[0])
// 1
println(b[0])
// 1
println(c[0])
// 1
```

If you set an item in the array to a new value with subscript syntax, all three of a, b, and c will return the new value. Note that the array is not copied when you set a new value with subscript syntax, because setting a single value with subscript syntax does not have the potential to change the array’s length:

如果通过下标语法修改数组中某一元素的值，那么a,b,c中的相应值都会发生改变。请注意当你用下标语法修改某一值时，并没有拷贝行为伴随发生，因为下表语法修改值时没有改变数组长度的可能：

```
a[0] = 42
println(a[0])
// 42
println(b[0])
// 42
println(c[0])
// 42
```

However, if you append a new item to a, you do modify the array’s length. This prompts Swift to create a new copy of the array at the point that you append the new value. Henceforth, a is a separate, independent copy of the array.

然而，当你给a附加新元素时，数组的长度发生改变。 Swift 会创建这个数组的一个拷贝。此后，a将会是一个独立拷贝。

If you change a value in a after the copy is made, a will return a different value from b and c, which both still reference the original array contents from before the copy took place:

拷贝发生后，如果再修改a中元素值的话，a将会返回与b，c不同的结果，因为后两者引用的是原来的数组：

```
a.append(4)
a[0] = 777
println(a[0])
// 777
println(b[0])
// 42
println(c[0])
// 42
```

#### Ensuring That an Array Is Unique

#### 确保数组的唯一性

It can be useful to ensure that you have a unique copy of an array before performing an action on that array’s contents, or before passing that array to a function or method. You ensure the uniqueness of an array reference by calling the unshare method on a variable of array type. (The unshare method cannot be called on a constant array.)

在操作一个数组，或将其传递给函数以及方法调用之前是很有必要先确定这个数组是有一个唯一拷贝的。通过在数组变量上调用unshare方法来确定数组引用的唯一性。(当数组赋给常量时，不能调用unshare方法)

If multiple variables currently refer to the same array, and you call the unshare method on one of those variables, the array is copied, so that the variable has its own independent copy of the array. However, no copying takes place if the variable is already the only reference to the array.

如果一个数组被多个变量引用，在其中的一个变量上调用unshare方法，则会拷贝此数组，此时这个变量将会有属于它自己的独立数组拷贝。当数组仅被一个变量引用时，则不会有拷贝发生。

At the end of the previous example, b and c both reference the same array. Call the unshare method on b to make it become a unique copy:

在上一个示例的最后，b和c都引用了同一个数组。此时在b上调用unshare方法则会将b变成一个唯一个拷贝：

```
b.unshare()
```

If you change the first value in b after calling the unshare method, all three arrays will now report a different value:

在unshare方法调用后再修改b中第一个元素的值，这三个数组(a,b,c)会返回不同的三个值：

```
b[0] = -105
println(a[0])
// 777
println(b[0])
// -105
println(c[0])
// 42
```

#### Checking Whether Two Arrays Share the Same Elements

#### 判定两个数组是否共用相同元素

Check whether two arrays or subarrays share the same storage and elements by comparing them with the identity operators (=== and !==).

我们通过使用恒等运算符(identity operators) (=== 和 !==)来判定两个数组或子数组共用相同的储存空间或元素。

The example below uses the “identical to” operator (===) to check whether b and c still share the same array elements:

下面这个示例使用了“等同(identical to)” 运算符(===) 来判定b和c是否共用相同的数组元素：

```
if b === c {
    println("b and c still share the same array elements.")
} else {
    println("b and c now refer to two independent sets of array elements.")
}
// prints "b and c now refer to two independent sets of array elements."
```

Alternatively, use the identity operators to check whether two subarrays share the same elements. The example below compares two identical subarrays from b and confirms that they refer to the same elements:

此外，我们还可以使用恒等运算符来判定两个子数组是否共用相同的元素。下面这个示例中，比较了b的两个相等的子数组，并且确定了这两个子数组都引用相同的元素：

```
if b[0...1] === b[0...1] {
    println("These two subarrays share the same elements.")
} else {
    println("These two subarrays do not share the same elements.")
}
// prints "These two subarrays share the same elements."
```

#### Forcing a Copy of an Array

#### 强制复制数组

Force an explicit copy of an array by calling the array’s copy method. This method performs a shallow copy of the array and returns a new array containing the copied items.

我们通过调用数组的copy方法进行强制显式复制。这个方法对数组进行了浅拷贝(shallow copy)，并且返回一个包含此拷贝数组的新数组。

The example below defines an array called names, which stores the names of seven people. A new variable called copiedNames is set to the result of calling the copy method on the names array:

下面这个示例中定义了一个names数组，其包含了七个人名。还定义了一个copiedNames变量，用以储存在names上调用copy方法所返回的结果：

```
var names = ["Mohsen", "Hilary", "Justyn", "Amy", "Rich", "Graham", "Vic"]
var copiedNames = names.copy()
```

You can prove that the names array has been copied by changing an item in one of the arrays and checking the corresponding item in the other. If you set the first item in the copiedNames array to "Mo" rather than "Mohsen", the names array still returns the old value of "Mohsen" from before the copy took place:

我们可以通过修改数组中某一个元素，并且检查另一个数组中对应元素的方法来判定names数组确已被复制。如果你将copiedNames中第一个元素从"Mohsen"修改为"Mo",则names数组返回的仍是拷贝发生前的"Mohsen"：

```
copiedNames[0] = "Mo"
println(names[0])
// prints "Mohsen"
```


> NOTE
> 
> If you simply need to be sure that your reference to an array’s contents is the only reference in existence, call the unshare method, not the copy method. The unshare method does not make a copy of the array unless it is necessary to do so. The copy method always copies the array, even if it is already unshared.

> 提示：
> 
> 如果你仅需要确保你对数组的引用是唯一引用，请调用unshare方法，而不是copy方法。unshare方法只在必要时才会创建数组拷贝。copy方法会在任何时候都创建一个新的拷贝，即使已经标记为唯一。