Extensions

Extensions add new functionality to an existing class, structure, or enumeration type. This includes the ability to extend types for which you do not have access to the original source code (known as retroactive modeling). Extensions are similar to categories in Objective-C. (Unlike Objective-C categories, Swift extensions do not have names.)
扩展为已有的类，结构，枚举添加新的功能。其中包括扩展没有访问权代码权限的类型（即追溯建模）。扩展和 Objective-C 当中的分类很相似。（与 Objective-C 中的分类不同的是，Swift 的扩展没有名字）


 Extensions in Swift can:
    Add computed properties and computed static properties
    Define instance methods and type methods
    Provide new initializers
    Define subscripts
    Define and use new nested types
    Make an existing type conform to a protocol

Swift 的扩展可以：
- 增加计算属性和静态计算属性
- 定义实例方法和类型方法
- 提供新的构造器
- 定义下标
- 定义和使用新的嵌套类型
- 将已有的类型转换为符合某一个协议


Note
If you define an extension to add new functionality to an existing type, the new functionality will be available on all existing instances of that type, even if they were created before the extension was defined.

注意
如果定义一个扩展用来在已有的类型上增加新的功能，那么新功能会应用在所有已经存在的实例上，即使是在扩展被定义之前实例化的。


Extension Syntax
Declare extensions with the extension keyword: 


扩展的语法
使用 extension 关键字来声明扩展

    extension SomeType {
        // new functionality to add to SomeType goes here
    }

An extension can extend an existing type to make it adopt one or more protocols. Where this is the case, the protocol names are written in exactly the same way as for a class or structure:
一个扩展可以扩展一个已有的类型，使它能适配一个或多个的协议。如果是这种情况的话，协议的命名方式应该与类和结构体的命名方式完全一致。

    extension SomeType: SomeProtocol, AnotherProtocol {
        // implementation of protocol requirements goes here
    }

Adding protocol conformance in this way is described in Adding Protocol Conformance with an Extension.
这种增加协议一致性的方式被称为通过扩展增加协议一致性


Computed Properties
计算属性

Extensions can add computed instance properties and computed type properties to existing types. This example adds five computed instance properties to Swift’s built-in Double type, to provide basic support for working with distance units: 
扩展可以为已有的类型增加计算实力属性和计算类型属性。这个例子向 Swift 内建类型 Double 添加五个计算实例类型，用来提供转换为距离单位的基本支持

    extension Double {
    var km: Double { return self * 1_000.0 }
    var m: Double { return self }
    var cm: Double { return self / 100.0 }
    var mm: Double { return self / 1_000.0 }
    var ft: Double { return self / 3.28084 }
    }
    let oneInch = 25.4.mm
    println("One inch is \(oneInch) meters")
    // prints "One inch is 0.0254 meters"
    let threeFeet = 3.ft
    println("Three feet is \(threeFeet) meters")
    // prints "Three feet is 0.914399970739201 meters"

These computed properties express that a Double value should be considered as a certain unit of length. Although they are implemented as computed properties, the names of these properties can be appended to a floating-point literal value with dot syntax, as a way to use that literal value to perform distance conversions. 
这些计算属性表达的是一个 Double 类型的值是某种长度单位下的值。尽管是计算属性，但他们仍然可以接在一个带有 dot 语法的字面值后面，用来将字面值转换成距离。

In this example, a Double value of 1.0 is considered to represent “one meter”. This is why the m computed property returns self—the expression 1.m is considered to calculate a Double value of 1.0. 
在上述的例子中，一个 Double 类型的值 1.0 代表“一米”。这是为什么计算属性 m 仅仅返回 self ——表达式 1.m 的值 Double 类型的值 1.0 。

Other units require some conversion to be expressed as a value measured in meters. One kilometer is the same as 1,000 meters, so the km computed property multiplies the value by 1_000.00 to convert into a number expressed in meters. Similarly, there are 3.28024 feet in a meter, and so the ft computed property divides the underlying Double value by 3.28024, to convert it from feet to meters. 
其他单位转换为以米为单位的数值需要进行一些转换。1千米等于1,000米，所以计算属性 km 要转换成以米为单位的数值，需要把值乘以 1_000.00 。同样，1英尺等于 3.28084 米，所以计算属性 ft 需要把值除以 3.28024 才能把英尺转换成米。

These properties are read-only computed properties, and so they are expressed without the get keyword, for brevity. Their return value is of type Double, and can be used within mathematical calculations wherever a Double is accepted: 
这些都是只读的计算属性，所以为了简便起见，不需要关键字 keyword 进行表示。他们的返回值都是 Double 类型的，所以可以用在所有可以接受 Double 类型的数学计算中：

    let aMarathon = 42.km + 195.m
    println("A marathon is \(aMarathon) meters long")
    // prints "A marathon is 42195.0 meters long"

Note
Extensions can add new computed properties, but they cannot add stored properties, or add property observers to existing properties.

注意
扩展可以添加新的计算属性，但是不能添加存储属性，也不能向已有属性添加属性观察器。



Initializers
构造器

Extensions can add new initializers to existing types. This enables you to extend other types to accept your own custom types as initializer parameters, or to provide additional initialization options that were not included as part of the type’s original implementation. 
扩展能向已有类型添加新的构造器。这允许你用自己定义的类型作为构造器参数扩展其他的类型，或者提供原始实现没有提供的额外的初始化选项

Extensions can add new convenience initializers to a class, but they cannot add new designated initializers or deinitializers to a class. Designated initializers and deinitializers must always be provided by the original class implementation. 
扩展能向类添加新的简便构造器，但是不能添加新的指定构造器或者析构器。指定构造器和析构器必须在类的原始实现中提供。


































