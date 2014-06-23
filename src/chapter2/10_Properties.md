# Properties
# 属性

Properties associate values with a particular class, structure, or enumeration. Stored properties store constant and variable values as part of an instance, whereas computed properties calculate (rather than store) a value. Computed properties are provided by classes, structures, and enumerations. Stored properties are provided only by classes and structures.

属性将值与特定的类，结构体或者枚举关联起来，存储属性将常量或变量值作为实力的一部分保存起来，而计算属性则用来计算(而非存储)一个值。计算属性可以用于类，结构体和枚举，存储属性只能用于类和结构体。


Stored and computed properties are usually associated with instances of a particular type. However, properties can also be associated with the type itself. Such properties are known as type properties.

存储和计算属性通常用于特定类型的实例。不过，属性也可以用于类型本身，这样的属性被称为类属性。


In addition, you can define property observers to monitor changes in a property’s value, which you can respond to with custom actions. Property observers can be added to stored properties you define yourself, and also to properties that a subclass inherits from its superclass.

另外，可以为属性定义监听器，以监听属性值的变化，这样就可以在属性值发生变化时触发自定义操作。可以在定义存储属性的时候为其添加属性监听器，也可以为子类继承父类的属性添加监听器。


## Stored Properties
## 存储属性

In its simplest form, a stored property is a constant or variable that is stored as part of an instance of a particular class or structure. Stored properties can be either variable stored properties (introduced by the var keyword) or constant stored properties (introduced by the let keyword).
简单而言，存储属性是一个特定类型实例或结构体中的常量或变量。存储属性可以是变量存储属性（用关键词 `var` 声明），也可以是常量属性（用关键词 `let` 声明）。


You can provide a default value for a stored property as part of its definition, as described in Default Property Values. You can also set and modify the initial value for a stored property during initialization. This is true even for constant stored properties, as described in Modifying Constant Properties During Initialization.

在定义存储属性时，可以为其指定默认值，详见 Default Property Values 。在存储属性初始化过程中，依然可以设置和修改它的初始值，甚至修改常量存储属性，详见 Modifying Constant Properties During Initialization。


The example below defines a structure called FixedLengthRange, which describes a range of integers whose range length cannot be changed once it is created:

下面的示例定义了一个名为 `FixedLengthRange` 的结构体，它表示一个整型的范围，其范围长度一旦创建不能改变：

    struct FixedLengthRange {
        var firstValue: Int
        let length: Int
    }
    var rangeOfThreeItems = FixedLengthRange(firstValue: 0, length: 3)
    // 表示整型值的范围为 0, 1, 2
    rangeOfThreeItems.firstValue = 6
    // 修改 firstValue 后, 表示的整型值的范围为: 6, 7, 8
    
Instances of FixedLengthRange have a variable stored property called firstValue and a constant stored property called length. In the example above, length is initialized when the new range is created and cannot be changed thereafter, because it is a constant property.

`FixedLengthRange` 的实例包含一个名为 `firstValue` 的变量存储属性和一个名为 `length` 常量存储属性。在上面的示例中， `length` 在 `FixedLengthRange` 实例创建时初始化，并且在此后不能被修改，因为它是一个常量属性。


###Stored Properties of Constant Structure Instances
###存储属性与常量实例


If you create an instance of a structure and assign that instance to a constant, you cannot modify the instance’s properties, even if they were declared as variable properties:

如果你为一个结构体创建一个实例， 并且把这个实例赋值给一个常量， 那么无论这个实例的属性是否为变量， 其属性都不能被修改。

    let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)
    // this range represents integer values 0, 1, 2, and 3
    // 表示取值范围为 整数的 0, 1, 2, 3
    rangeOfFourItems.firstValue = 6
    // this will report an error, even thought firstValue is a variable property
    // 尽管firstValue是变量属性, 对其赋值也会报错

Because rangeOfFourItems is declared as a constant (with the let keyword), it is not possible to change its firstValue property, even though firstValue is a variable property.
This behavior is due to structures being value types. When an instance of a value type is marked as a constant, so are all of its properties.

因为 `rangeOfFourItems`通过`let`关键词声明， 所以是个常量， 故， 无论它的属性是否为变量， 都无法改变它的属性值。 所以， 当一个实例是常量类型， 那么它的所有属性也会变成常量类型。


The same is not true for classes, which are reference types. If you assign an instance of a reference type to a constant, you can still change that instance’s variable properties.

这种情况对于引用类型(类)并不适用。 如果将某个引用类型的实例赋值给一个常量， 那么依然可以修改该实例的属性。

###Lazy Stored Properties
###惰性存储属性


A lazy stored property is a property whose initial value is not calculated until the first time it is used. You indicate a lazy stored property by writing the @lazy attribute before its declaration.

惰性存储属性只有在首次调用时才会进行初始化。 通过在存储属性声明前加上 `@lazy` 来声明一个惰性存储属性。

> NOTE
You must always declare a lazy property as a variable (with the var keyword), because its initial value may not be retrieved until after instance initialization completes. Constant properties must always have a value before initialization completes, and therefore cannot be declared as lazy.

> 注意
在声明一个惰性存储属性时， 必须将其定义为变量(通过`var`声明)。 这样做的原因是， 在实例初始化完成前， 可能无法获得惰性属性的初始值。 相反的， 常量属性的初始值必须在实例初始化完成之前赋值，所以常量属性不能被声明为惰性属性。

Lazy properties are useful when the initial value for a property is dependent on outside factors whose values are not known until after an instance’s initialization is complete. Lazy properties are also useful when the initial value for a property requires complex or computationally expensive setup that should not be performed unless or until it is needed.

当某个属性的初始化依赖于其他实例的初始化时，惰性属性是非常有用的。惰性属性在需要复杂计算和耗费时间较长的属性初始化时，也是非常有用的，因为它可以在需要时再进行计算和初始化。

The example below uses a lazy stored property to avoid unnecessary initialization of a complex class. This example defines two classes called DataImporter and DataManager, neither of which is shown in full:

下面这个例子中，演示了在一个复杂类的初始化过程中，如何通过惰性存储属性来避免不必要的初始化。示例中定义了两个类：`DataImporter`, `DataManager`（代码片段）。

    class DataImporter {
        /*
        DataImporter is a class to import data from an external file.
        The class is assumed to take a non-trivial amount of time to initialize.
        
        DataImporter 是一个可以从外部文件导入数据的类
        该类的初始化会消耗很长一段时间
        
        */
        var fileName = "data.txt"
        // the DataImporter class would provide data importing functionality here
        // 这里是DataImporter类导入数据的代码
    }
     
    class DataManager {
        @lazy var importer = DataImporter()
        var data = String[]()
        // the DataManager class would provide data management functionality here
        // DataManager类数据管理功能的代码
    }
      
    let manager = DataManager()
    manager.data += "Some data"
    manager.data += "Some more data"
    // the DataImporter instance for the importer property has not yet been created
    // importer 实例尚未初始化


The DataManager class has a stored property called data, which is initialized with a new, empty array of String values. Although the rest of its functionality is not shown, the purpose of this DataManager class is to manage and provide access to this array of String data.

`DataManager` 类拥有一个名为 `data` 的存储属性，该属性是一个空的字符串数组。虽然剩余的功能代码没有展示出来，不过 `DataManager` 类的目的是提供管理和访问该字符串数组的功能。


Part of the functionality of the DataManager class is the ability to import data from a file. This functionality is provided by the DataImporter class, which is assumed to take a non-trivial amount of time to initialize. This might be because a DataImporter instance needs to open a file and read its contents into memory when the DataImporter instance is initialized.

`DataManager`类的一个功能是从文件中导入数据。 该功能由 `DataImporter` 类提供，需要花费很长时间进行初始化。原因是 `DataImporter` 类的实例在初始化的时候需要读取文件并将文件内容写入内存。

It is possible for a DataManager instance to manage its data without ever importing data from a file, so there is no need to create a new DataImporter instance when the DataManager itself is created. Instead, it makes more sense to create the DataImporter instance if and when it is first used.

对于 `DataManager` 类来说，无论是从文件中导入了数据，都不影响它管理自己的数据，所以没必要在它自己初始化的时候就去创建 `DataManager` 实例。更好的做法是，将 `DataImporter` 实例在第一次使用的时候初始化。


Because it is marked with the @lazy attribute, the DataImporter instance for the importer property is only created when the importer property is first accessed, such as when its fileName property is queried:

因为使用了 `@lazy`，故 `DataImporter` 的实例 `importer` 只会在 `importer`的实例第一次被访问的时候才会初始化，例如访问它的 `fileName` 属性：

println(manager.importer.fileName)
// the DataImporter instance for the importer property has now been created
//此时， `DataImporter` 的实例 `importer` 才被创建
// prints "data.txt"

###Stored Properties and Instance Variables

###存储属性和实例变量


If you have experience with Objective-C, you may know that it provides two ways to store values and references as part of a class instance. In addition to properties, you can use instance variables as a backing store for the values stored in a property.

`Object-C`中类的实例对象有两种存储值和引用的方法。除了属性，还可以使用实例变量保存值。

Swift unifies these concepts into a single property declaration. A Swift property does not have a corresponding instance variable, and the backing store for a property is not accessed directly. This approach avoids confusion about how the value is accessed in different contexts and simplifies the property’s declaration into a single, definitive statement. All information about the property including its name, type, and memory management characteristics—is defined in a single location as part of the type’s definition.

在`Swift`中没有实例变量，`Swift` 将这些概念统一为了属性。这样避免了在不同上下文中值的不同访问方式的混淆，并且使属性声明简单明了。所有的属性信息：名称，类型，内存管理特征都包含在类型定义中。

##Computed Properties

##计算属性


In addition to stored properties, classes, structures, and enumerations can define computed properties, which do not actually store a value. Instead, they provide a getter and an optional setter to retrieve and set other properties and values indirectly.

除了存储属性外，类，结构体，枚举还可以定义计算属性。计算属性不能存储值，而是通过 `getter` 方法和 `setter` 方法（可选）间接的设置其他属性和值。

    struct Point {
        var x = 0.0, y = 0.0
    }
    struct Size {
        var width = 0.0, height = 0.0
    }
    struct Rect {
        var origin = Point()
        var size = Size()
        var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
        }
    }
    var square = Rect(origin: Point(x: 0.0, y: 0.0),
        size: Size(width: 10.0, height: 10.0))
    let initialSquareCenter = square.center
    square.center = Point(x: 15.0, y: 15.0)
    println("square.origin is now at (\(square.origin.x), \(square.origin.y))")
    // prints "square.origin is now at (10.0, 10.0)"
    // 输出 "square.origin is now at (10.0, 10.0)"

This example defines three structures for working with geometric shapes:

这个示例定义了三个结构体来表示一个几何形状:

Point encapsulates an (x, y) coordinate.
`Point` 封装了坐标(x, y)。

Size encapsulates a width and a height.

`Size` 封装了宽度和高度。

Rect defines a rectangle by an origin point and a size.

`Rect` 用坐标原点和大小定义了一个矩形。

The Rect structure also provides a computed property called center. The current center position of a Rect can always be determined from its origin and size, and so you don’t need to store the center point as an explicit Point value. Instead, Rect defines a custom getter and setter for a computed variable called center, to enable you to work with the rectangle’s center as if it were a real stored property.

`Rect` 结构体提供了一个名为 `center` 的计算属性。矩形的中心点总是可以通过它的原点坐标和大小计算出来，所以你没有必要保存一个确切的矩形中心点的值。这里的 `Rect` 为一个名为 `center` 的计算属性定义了自定义的 `getter` 和 `setter` 方法，以此来设置矩形的中心点。

The preceding example creates a new Rect variable called square. The square variable is initialized with an origin point of (0, 0), and a width and height of 10. This square is represented by the blue square in the diagram below.

例子中接下来创建了一个名为 `square` 的 `Rect` 实例，`point` 初始值为(0,0)， `width` 和 `height` 都是10，在下图中用蓝色正方形表示。

The square variable’s center property is then accessed through dot syntax (square.center), which causes the getter for center to be called, to retrieve the current property value. Rather than returning an existing value, the getter actually calculates and returns a new Point to represent the center of the square. As can be seen above, the getter correctly returns a center point of (5, 5).

然后通过点运算符（`square.center`）访问了 `square` 实例的 `center` 属性，此时会触发 `center` 的 `getter` 方法，并返回当前的属性值。和直接返回值不同， `getter` 方法会计算并返回最新的属性值。从上面的代码可以看出， `getter` 方法正确的返回了中心点 `(5, 5)`。


The center property is then set to a new value of (15, 15), which moves the square up and to the right, to the new position shown by the orange square in the diagram below. Setting the center property calls the setter for center, which modifies the x and y values of the stored origin property, and moves the square to its new position.

接着为 `center` 属性设置了新值 `(15, 15)`，在下图中可以看出 `square` 向右上移动到了一个新的位置（橙色区域）。在设置 `center` 属性时调用了它的 `setter` 方法，修改了 `origin` 的 `x,y`值，并且改变了 `square` 的位置。

![Alt text](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/computedProperties_2x.png)


###Shorthand Setter Declaration

###Setter声明简写

If a computed property’s setter does not define a name for the new value to be set, a default name of newValue is used. Here’s an alternative version of the Rect structure, which takes advantage of this shorthand notation:

如果没有给属性的 `setter` 方法的新值指定名称，那么可以使用默认值 `newValue` 。下面是 `Rect` 结构体的简写形式：

    struct AlternativeRect {
        var origin = Point()
        var size = Size()
        var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set {
            origin.x = newValue.x - (size.width / 2)
            origin.y = newValue.y - (size.height / 2)
        }
        }
    }


###Read-Only Computed Properties

###只读计算属性

A computed property with a getter but no setter is known as a read-only computed property. A read-only computed property always returns a value, and can be accessed through dot syntax, but cannot be set to a different value.

只有 `getter` 没有 `setter` 的计算属性是只读计算属性。只读计算属性可以通过点操作符访问，但不能为其设置其他值。


> NOTE

> You must declare computed properties—including read-only computed properties—as variable properties with the var keyword, because their value is not fixed. The let keyword is only used for constant properties, to indicate that their values cannot be changed once they are set as part of instance initialization.


> 注意

> 必须使用 `var` 关键词定义计算属性，包括只读计算属性，因为它们的值是可能改变的。 `let` 关键词只用于常量属性，其值在初始化后不可改变。

必须使用var关键字定义计算属性，包括只读计算属性，因为他们的值不是固定的。let关键字只用来声明常量属性，表示初始化后再也无法修改的值。


You can simplify the declaration of a read-only computed property by removing the get keyword and its braces:

只读计算属性的声明可以去掉get关键词和花括号：

    struct Cuboid {
        var width = 0.0, height = 0.0, depth = 0.0
        var volume: Double {
        return width * height * depth
        }
    }

    let fourByFiveByTwo = Cuboid(width: 4.0, height: 5.0, depth: 2.0)
    println("the volume of fourByFiveByTwo is \(fourByFiveByTwo.volume)")
    // prints "the volume of fourByFiveByTwo is 40.0"
    // 输出 "the volume of fourByFiveByTwo is 40.0"

This example defines a new structure called Cuboid, which represents a 3D rectangular box with width, height, and depth properties. This structure also has a read-only computed property called volume, which calculates and returns the current volume of the cuboid. It doesn’t make sense for volume to be settable, because it would be ambiguous as to which values of width, height, and depth should be used for a particular volume value. Nonetheless, it is useful for a Cuboid to provide a read-only computed property to enable external users to discover its current calculated volume.

这个示例定义了一个名为 `Cuboid` 的结构体，表示一个3D的立方体，有 `width`，`height`，`depth`等属性。它还有一个名为 `volume` 的只读计算属性用来计算并返回 `cuboid` 当前的体积。我们没有必要去设置 `volume` 的值，因为 `volume` 的值可以通过 `width`，`height`，`depth`计算出来。所以比较合适的做法是，提供一个只读计算属性让用户可以获得当前的 `volume` 。


###Property Observers

###属性观察者

Property observers observe and respond to changes in a property’s value. Property observers are called every time a property’s value is set, even if the new value is the same as the property’s current value.

属性观察者用来观察并响应属性值的变化。在为属性赋值时，无论新值是否与原值相同，都会触发属性的观察者。

You can add property observers to any stored properties you define, apart from lazy stored properties. You can also add property observers to any inherited property (whether stored or computed) by overriding the property within a subclass. Property overriding is described in Overriding.

可以为除了惰性属性外的其他任何存储属性定义观察者。通过属性重写，可以在子类中为它的父类属性（无论是存储或是计算属性）添加观察者。属性重写在重写一章有详细介绍。


> NOTE
> 
> You don’t need to define property observers for non-overridden
> computed properties, because you can observe and respond to changes to
> their value from directly within the computed property’s setter.

> 注意
> 
> 不需要为非重写计算属性定义观察者，因为你可以直接使用计算属性的`setter`来完成。


You have the option to define either or both of these observers on a property:
* willSet is called just before the value is stored.
* didSet is called immediately after the new value is stored.

可以通过两种方式为属性定义观察者:
* `willSet` 在值发生改变之前调用
* `didSet` 在值发生改变之后调用


If you implement a willSet observer, it is passed the new property value as a constant parameter. You can specify a name for this parameter as part of your willSet implementation. If you choose not to write the parameter name and parentheses within your implementation, the parameter will still be made available with a default parameter name of newValue.

`willSet` 会将新属性值作为常量参数，并且可以为该常量参数指定名称。如果没有为该参数指定名称，那么会使用默认的参数名称 `newValue`。


Similarly, if you implement a didSet observer, it will be passed a constant parameter containing the old property value. You can name the parameter if you wish, or use the default parameter name of oldValue.

与 `willSet` 类似，`didSet` 会将原属性值作为常量参数。同样可以为参数指定名称或者使用默认值 `oldValue`。

> NOTE
> 
> willSet and didSet observers are not called when a property is first
> initialized. They are only called when the property’s value is set
> outside of an initialization context.

> 注意
> 
> `willSet` 和 `didSet` 在属性初始化时不会被调用。

Here’s an example of willSet and didSet in action. The example below defines a new class called StepCounter, which tracks the total number of steps that a person takes while walking. This class might be used with input data from a pedometer or other step counter to keep track of a person’s exercise during their daily routine.

这里有一个使用了 `willSet` 和 `didSet` 的示例。示例中定义了一个名为 `StepCounter` 的类，用来统计当人步行时的总步数，通过使用计步器等装置可以用这个类追踪人在日常工作中的运动量。

    class StepCounter {
        var totalSteps: Int = 0 {
            willSet(newTotalSteps) {
                println("About to set totalSteps to \(newTotalSteps)")
            }
            didSet {
                if totalSteps > oldValue  {
                    println("Added \(totalSteps - oldValue) steps")
                }
            }
        }
    }
    let stepCounter = StepCounter()
    stepCounter.totalSteps = 200
    // About to set totalSteps to 200
    // Added 200 steps
    // 输出 About to set totalSteps to 200
    // 输出 Added 200 steps
    stepCounter.totalSteps = 360
    // About to set totalSteps to 360
    // Added 160 steps
    // 输出 About to set totalSteps to 360
    // 输出 Added 160 steps
    stepCounter.totalSteps = 896
    // About to set totalSteps to 896
    // Added 536 steps
    // 输出 About to set totalSteps to 896
    // 输出 Added 536 steps
    
The StepCounter class declares a totalSteps property of type Int. This is a stored property with willSet and didSet observers.

`StepCounter`定义了一个 `int` 类型的属性 `totalSteps`。 `totalSteps` 包含了两个观察者`willSet`和`didSet`。


The willSet and didSet observers for totalSteps are called whenever the property is assigned a new value. This is true even if the new value is the same as the current value.

当`totalSteps`的值改变时（不论新值是否与原值相同），`willSet` 和 `didSet` 都会被调用。


This example’s willSet observer uses a custom parameter name of newTotalSteps for the upcoming new value. In this example, it simply prints out the value that is about to be set.

示例中的`willSet`使用了一个名为`newTotalSteps`的参数接收新值。在这个例子中只是简单的将新值输出。


The didSet observer is called after the value of totalSteps is updated. It compares the new value of totalSteps against the old value. If the total number of steps has increased, a message is printed to indicate how many new steps have been taken. The didSet observer does not provide a custom parameter name for the old value, and the default name of oldValue is used instead.

`didSet`观察者会在`totalSteps`的值被修改后调用。它将`totalSteps`的新值与原值做比较，如果新值大于原值，则会输出新增了多少步。`didSet`观察者没有指定参数名，所以使用默认参数名`oldValue`。


> NOTE
> 
> If you assign a value to a property within its own didSet observer,
> the new value that you assign will replace the one that was just set.


> 注意

> 如果在`didSet`中给属性设置新值，那么新值会替换刚刚设置的值。

##Global and Local Variables

##全局变量和局部变量


The capabilities described above for computing and observing properties are also available to global variables and local variables. Global variables are variables that are defined outside of any function, method, closure, or type context. Local variables are variables that are defined within a function, method, or closure context.

上面关于属性的计算和观察功能对于全局变量和局部变量同样适用。全局变量定义在所有函数，方法，闭包，类型之外。局部变量定义在函数，方法或闭包内部。


The global and local variables you have encountered in previous chapters have all been stored variables. Stored variables, like stored properties, provide storage for a value of a certain type and allow that value to be set and retrieved.

在前面的章节中全局和局部变量都是存储变量，类似于存储属性，它为特定类型的值提供存储空间，并允许对其进行读写。


However, you can also define computed variables and define observers for stored variables, in either a global or local scope. Computed variables calculate rather than store a value, and are written in the same way as computed properties.

另外，还可以在全局或局部作用域中定义计算变量，或者为存储变量定义观察者。计算变量用来计算而非存储一个值，声明方式和计算属性一样。


> NOTE
> 
> Global constants and variables are always computed lazily, in a
> similar manner to Lazy Stored Properties. Unlike lazy stored
> properties, global constants and variables do not need to be marked
> with the @lazy attribute.
> 
> Local constants and variables are never computed lazily.


> 注意
> 
> 和惰性存储属性的方式类似，全局常量和变量总是延迟计算的。不同的是，全局常量和变量不需要使用`@lazy`属性进行声明。
> 
> 局部常量和变量则绝不会延迟计算。


##Type Properties

##类型属性


Instance properties are properties that belong to an instance of a particular type. Every time you create a new instance of that type, it has its own set of property values, separate from any other instance.

实例属性属于一个特定类型的实例。每次创建该类型的实例，它都拥有自己独立的一组属性，与其他实例对象无关。


You can also define properties that belong to the type itself, not to any one instance of that type. There will only ever be one copy of these properties, no matter how many instances of that type you create. These kinds of properties are called type properties.

还可以定义属于类型自身的属性。不论该类型有多少实例，这些属性都只有一份。这种属性被称为类型属性。


Type properties are useful for defining values that are universal to all instances of a particular type, such as a constant property that all instances can use (like a static constant in C), or a variable property that stores a value that is global to all instances of that type (like a static variable in C).

类型属性用于定义所有特定的类型实例都可以使用的值，比如所有实例都可以使用同一个常量属性（类似于`C`中的静态常量），或者就像所有的实例都可以使用全局变量属性（类似于`C`中的静态常量）。


For value types (that is, structures and enumerations), you can define stored and computed type properties. For classes, you can define computed type properties only.

对于值类型（结构和枚举），可以定义存储和计算类型的属性。对于类，则只能定义计算类型的属性。


Stored type properties for value types can be variables or constants. Computed type properties are always declared as variable properties, in the same way as computed instance properties.

值类型的存储类型属性可以是变量和常量。计算类型属性和计算实例属性相同，通常声明为变量属性。

> NOTE
> 
> Unlike stored instance properties, you must always give stored type
> properties a default value. This is because the type itself does not
> have an initializer that can assign a value to a stored type property
> at initialization time.

> 注意
> 
> 与存储实例属性不同，必须为存储类型属性定义默认值。原因是类型本身没有一个可以在初始化时为类型属性赋值的构造器。


###Type Property Syntax

###类型属性语法


In C and Objective-C, you define static constants and variables associated with a type as global static variables. In Swift, however, type properties are written as part of the type’s definition, within the type’s outer curly braces, and each type property is explicitly scoped to the type it supports.

在`C`和`Objective-C`中，只能使用全局静态变量来定义依赖于某个属性的变量或常量。但在`Swift`中，类型属性可以作为类型定义的一部分，它的作用域也在类型的范围内。    


You define type properties for value types with the static keyword, and type properties for class types with the class keyword. The example below shows the syntax for stored and computed type properties:

使用`static`关键词定义值类型的类型属性，`class`类型的类型属性用关键词`class`声明。下面的示例演示了存储类型属性和计算类型属性的语法：


    struct SomeStructure {
        static var storedTypeProperty = "Some value."
        static var computedTypeProperty: Int {
        // return an Int value here
        // 这里将返回一个`Int`的值
        }
    }
    enum SomeEnumeration {
        static var storedTypeProperty = "Some value."
        static var computedTypeProperty: Int {
        // return an Int value here
        // 这里将返回一个`Int`的值
        }
    }
    class SomeClass {
        class var computedTypeProperty: Int {
        // return an Int value here
        // 这里将返回一个`Int`的值
        }
    }
    

> NOTE
> 
> The computed type property examples above are for read-only computed
> type properties, but you can also define read-write computed type
> properties with the same syntax as for computed instance properties.

注意

上面的计算类型属性的示例都是只读的，仍然可以定义可读写的计算类型属性。


###Querying and Setting Type Properties

###查询和设置类型属性


Type properties are queried and set with dot syntax, just like instance properties. However, type properties are queried and set on the type, not on an instance of that type. For example:

就像实例属性，类型属性通过点操作符查询和设置。不过，类型属性的是通过类型自身查询和设置，而非类型的实例：

    println(SomeClass.computedTypeProperty)
    // prints "42"
    // 输出 "42"
    
    println(SomeStructure.storedTypeProperty)
    // prints "Some value."
    // 输出 "Some value."
    SomeStructure.storedTypeProperty = "Another value."
    println(SomeStructure.storedTypeProperty)
    // prints "Another value."
    // 输出 "Another value."

The examples that follow use two stored type properties as part of a structure that models an audio level meter for a number of audio channels. Each channel has an integer audio level between 0 and 10 inclusive.

下面的示例定义了一个结构体和两个类型属性来为声道音量建模。每一个声道的音量范围是0到10。


The figure below illustrates how two of these audio channels can be combined to model a stereo audio level meter. When a channel’s audio level is 0, none of the lights for that channel are lit. When the audio level is 10, all of the lights for that channel are lit. In this figure, the left channel has a current level of 9, and the right channel has a current level of 7:

下图演示了如何将两个声道合并为一个立体声道。当某个声道的音量值是0时，所有灯都不会亮。当音量值是10时，所有灯都会亮起。下图中，左侧的音量值为9，右侧的音量值为7：


![Alt text](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/staticPropertiesVUMeter_2x.png)

The audio channels described above are represented by instances of the AudioChannel structure:

上面的声道通过`AudioChannel`的结构体实例表示如下：

    struct AudioChannel {
        static let thresholdLevel = 10
        static var maxInputLevelForAllChannels = 0
        var currentLevel: Int = 0 {
        didSet {
            if currentLevel > AudioChannel.thresholdLevel {
                // cap the new audio level to the threshold level
                // 将音量值设置为最大值
                currentLevel = AudioChannel.thresholdLevel
            }
            if currentLevel > AudioChannel.maxInputLevelForAllChannels {
                // store this as the new overall maximum input level
                // 将音量值设置为当前值
                AudioChannel.maxInputLevelForAllChannels = currentLevel
            }
        }
        }
    }

The AudioChannel structure defines two stored type properties to support its functionality. The first, thresholdLevel, defines the maximum threshold value an audio level can take. This is a constant value of 10 for all AudioChannel instances. If an audio signal comes in with a higher value than 10, it will be capped to this threshold value (as described below).

`AudioChannel`定义了两个存储属性。首先，定义了音量最大值`thresholdLevel`，它是一个对所有实例可见的常量值。如果音量大于10，那么就取上限值10。


The second type property is a variable stored property called maxInputLevelForAllChannels. This keeps track of the maximum input value that has been received by any AudioChannel instance. It starts with an initial value of 0.

第二个类型属性是一个名为`maxInputLevelForAllChannels`的变量存储属性，用来表示所有实例的最大音量值。初始值为0。


The AudioChannel structure also defines a stored instance property called currentLevel, which represents the channel’s current audio level on a scale of 0 to 10.

`AudioChannel`结构体还定义了一个实例属性`currentLevel`，用来表示当前声道的音量值，取值0到10。


The currentLevel property has a didSet property observer to check the value of currentLevel whenever it is set. This observer performs two checks:


`currentLevel`的值在每次设置时都会通过`didSet`进行两种检查：

* If the new value of currentLevel is greater than the allowed thresholdLevel, the property observer caps currentLevel to thresholdLevel.
* If the new value of currentLevel (after any capping) is higher than any value previously received by any AudioChannel instance, the property observer stores the new currentLevel value in the maxInputLevelForAllChannels static property.

* 如果`currentLevel`的新值大于允许的最大值`thresholdLevel`，则属性监听器将`currentLevel`设置为`thresholdLevel`。
* 如果`currentLevel`的新值大于之前所有`AudioChannel`实例的值。那么属性监听器会将新值保存在静态属性`maxInputLevelForAllChannels`中。


> NOTE
> 
> In the first of these two checks, the didSet observer sets
> currentLevel to a different value. This does not, however, cause the
> observer to be called again.

> 注意
> 
> 在第一次检查过程中，`didSet`监听器将`currentLevel`设置为了不同的值，但此时不会再次调用属性监听器。


You can use the AudioChannel structure to create two new audio channels called leftChannel and rightChannel, to represent the audio levels of a stereo sound system:

可以使用`AudioChannel`创建两个声道实例：`leftChannel`和`rightChannel`：

    var leftChannel = AudioChannel()
    var rightChannel = AudioChannel()
    
If you set the currentLevel of the left channel to 7, you can see that the maxInputLevelForAllChannels type property is updated to equal 7:
    

如果将`currentLevel`的左声道的值置为7，则可以看到类型属性`maxInputLevelForAllChannels`也更新为了7：

    leftChannel.currentLevel = 7
    println(leftChannel.currentLevel)
    // prints "7"
    // 输出 "7"
    println(AudioChannel.maxInputLevelForAllChannels)
    // print "7"
    // 输出 "7"

If you try to set the currentLevel of the right channel to 11, you can see that the right channel’s currentLevel property is capped to the maximum value of 10, and the maxInputLevelForAllChannels type property is updated to equal 10:

如果想将`currentLevel`的右声道设置为11，你会发现右声道的`currentLevel`值被设置为了10，同时`maxInputLevelForAllChannels` 也更新为10。


    rightChannel.currentLevel = 11
    println(rightChannel.currentLevel)
    // prints "10"
    // 输出 "10"
    println(AudioChannel.maxInputLevelForAllChannels)
    // prints "10"
    // 输出 "10"