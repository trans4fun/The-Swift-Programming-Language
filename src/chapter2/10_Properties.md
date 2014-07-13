# 属性

属性将值与特定的类，结构体或者枚举关联起来，存储属性将常量或变量值作为实力的一部分保存起来，而计算属性则用来计算(而非存储)一个值。计算属性可以用于类，结构体和枚举，存储属性只能用于类和结构体。

存储和计算属性通常用于特定类型的实例。不过，属性也可以用于类型本身，这样的属性被称为类属性。

另外，可以为属性定义监听器，以监听属性值的变化，这样就可以在属性值发生变化时触发自定义操作。可以在定义存储属性的时候为其添加属性监听器，也可以为子类继承父类的属性添加监听器。


## 存储属性

简单而言，存储属性是一个特定类型实例或结构体中的常量或变量。存储属性可以是变量存储属性（用关键词 `var` 声明），也可以是常量属性（用关键词 `let` 声明）。

在定义存储属性时，可以为其指定默认值，详见 《构造过程 - 默认属性值》。在存储属性初始化过程中，依然可以设置和修改它的初始值，甚至修改常量存储属性，详见 《构造过程 - 在构造过程中修改恒定属性》。

下面的示例定义了一个名为 `FixedLengthRange` 的结构体，它表示一个整型的范围，其范围长度一旦创建不能改变：

    struct FixedLengthRange {
        var firstValue: Int
        let length: Int
    }
    var rangeOfThreeItems = FixedLengthRange(firstValue: 0, length: 3)
    // 表示整型值的范围为 0, 1, 2
    rangeOfThreeItems.firstValue = 6
    // 修改 firstValue 后, 表示的整型值的范围为: 6, 7, 8
    
`FixedLengthRange` 的实例包含一个名为 `firstValue` 的变量存储属性和一个名为 `length` 常量存储属性。在上面的示例中， `length` 在 `FixedLengthRange` 实例创建时初始化，并且在此后不能被修改，因为它是一个常量属性。


###存储属性与常量实例

如果你为一个结构体创建一个实例， 并且把这个实例赋值给一个常量， 那么无论这个实例的属性是否为变量， 其属性都不能被修改。

    let rangeOfFourItems = FixedLengthRange(firstValue: 0, length: 4)
    // this range represents integer values 0, 1, 2, and 3
    // 表示取值范围为 整数的 0, 1, 2, 3
    rangeOfFourItems.firstValue = 6
    // this will report an error, even thought firstValue is a variable property
    // 尽管firstValue是变量属性, 对其赋值也会报错

因为 `rangeOfFourItems`通过`let`关键词声明， 所以是个常量， 故， 无论它的属性是否为变量， 都无法改变它的属性值。 所以， 当一个实例是常量类型， 那么它的所有属性也会变成常量类型。

这种情况对于引用类型(类)并不适用。 如果将某个引用类型的实例赋值给一个常量， 那么依然可以修改该实例的属性。

###惰性存储属性

惰性存储属性只有在首次调用时才会进行初始化。 通过在存储属性声明前加上 `@lazy` 来声明一个惰性存储属性。

> 注意
在声明一个惰性存储属性时， 必须将其定义为变量(通过`var`声明)。 这样做的原因是， 在实例初始化完成前， 可能无法获得惰性属性的初始值。 相反的， 常量属性的初始值必须在实例初始化完成之前赋值，所以常量属性不能被声明为惰性属性。

当某个属性的初始化依赖于其他实例的初始化时，惰性属性是非常有用的。惰性属性在需要复杂计算和耗费时间较长的属性初始化时，也是非常有用的，因为它可以在需要时再进行计算和初始化。

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

`DataManager` 类拥有一个名为 `data` 的存储属性，该属性是一个空的字符串数组。虽然剩余的功能代码没有展示出来，不过 `DataManager` 类的目的是提供管理和访问该字符串数组的功能。

`DataManager`类的一个功能是从文件中导入数据。 该功能由 `DataImporter` 类提供，需要花费很长时间进行初始化。原因是 `DataImporter` 类的实例在初始化的时候需要读取文件并将文件内容写入内存。

对于 `DataManager` 类来说，无论是从文件中导入了数据，都不影响它管理自己的数据，所以没必要在它自己初始化的时候就去创建 `DataManager` 实例。更好的做法是，将 `DataImporter` 实例在第一次使用的时候初始化。

因为使用了 `@lazy`，故 `DataImporter` 的实例 `importer` 只会在 `importer`的实例第一次被访问的时候才会初始化，例如访问它的 `fileName` 属性：

println(manager.importer.fileName)
// the DataImporter instance for the importer property has now been created
//此时， `DataImporter` 的实例 `importer` 才被创建
// prints "data.txt"

###存储属性和实例变量

`Object-C`中类的实例对象有两种存储值和引用的方法。除了属性，还可以使用实例变量保存值。

在`Swift`中没有实例变量，`Swift` 将这些概念统一为了属性。这样避免了在不同上下文中值的不同访问方式的混淆，并且使属性声明简单明了。所有的属性信息：名称，类型，内存管理特征都包含在类型定义中。

##计算属性

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

这个示例定义了三个结构体来表示一个几何形状:

`Point` 封装了坐标(x, y)。

`Size` 封装了宽度和高度。

`Rect` 用坐标原点和大小定义了一个矩形。

`Rect` 结构体提供了一个名为 `center` 的计算属性。矩形的中心点总是可以通过它的原点坐标和大小计算出来，所以你没有必要保存一个确切的矩形中心点的值。这里的 `Rect` 为一个名为 `center` 的计算属性定义了自定义的 `getter` 和 `setter` 方法，以此来设置矩形的中心点。

例子中接下来创建了一个名为 `square` 的 `Rect` 实例，`point` 初始值为(0,0)， `width` 和 `height` 都是10，在下图中用蓝色正方形表示。

然后通过点运算符（`square.center`）访问了 `square` 实例的 `center` 属性，此时会触发 `center` 的 `getter` 方法，并返回当前的属性值。和直接返回值不同， `getter` 方法会计算并返回最新的属性值。从上面的代码可以看出， `getter` 方法正确的返回了中心点 `(5, 5)`。

接着为 `center` 属性设置了新值 `(15, 15)`，在下图中可以看出 `square` 向右上移动到了一个新的位置（橙色区域）。在设置 `center` 属性时调用了它的 `setter` 方法，修改了 `origin` 的 `x,y`值，并且改变了 `square` 的位置。

![Alt text](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/computedProperties_2x.png)


###Setter声明简写

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


###只读计算属性

只有 `getter` 没有 `setter` 的计算属性是只读计算属性。只读计算属性可以通过点操作符访问，但不能为其设置其他值。

> 注意

> 必须使用 `var` 关键词定义计算属性，包括只读计算属性，因为它们的值是可能改变的。 `let` 关键词只用于常量属性，其值在初始化后不可改变。

必须使用var关键字定义计算属性，包括只读计算属性，因为他们的值不是固定的。let关键字只用来声明常量属性，表示初始化后再也无法修改的值。

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

这个示例定义了一个名为 `Cuboid` 的结构体，表示一个3D的立方体，有 `width`，`height`，`depth`等属性。它还有一个名为 `volume` 的只读计算属性用来计算并返回 `cuboid` 当前的体积。我们没有必要去设置 `volume` 的值，因为 `volume` 的值可以通过 `width`，`height`，`depth`计算出来。所以比较合适的做法是，提供一个只读计算属性让用户可以获得当前的 `volume` 。

###属性观察者

属性观察者用来观察并响应属性值的变化。在为属性赋值时，无论新值是否与原值相同，都会触发属性的观察者。

可以为除了惰性属性外的其他任何存储属性定义观察者。通过属性重写，可以在子类中为它的父类属性（无论是存储或是计算属性）添加观察者。属性重写在《构造过程 - 构造方法的继承与重写》一章中有详细介绍。

> 注意
> 
> 不需要为非重写计算属性定义观察者，因为你可以直接使用计算属性的`setter`来完成。

可以通过两种方式为属性定义观察者:
* `willSet` 在值发生改变之前调用
* `didSet` 在值发生改变之后调用

`willSet` 会将新属性值作为常量参数，并且可以为该常量参数指定名称。如果没有为该参数指定名称，那么会使用默认的参数名称 `newValue`。

与 `willSet` 类似，`didSet` 会将原属性值作为常量参数。同样可以为参数指定名称或者使用默认值 `oldValue`。

> 注意
> 
> `willSet` 和 `didSet` 在属性初始化时不会被调用。

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
    
`StepCounter`定义了一个 `int` 类型的属性 `totalSteps`。 `totalSteps` 包含了两个观察者`willSet`和`didSet`。

当`totalSteps`的值改变时（不论新值是否与原值相同），`willSet` 和 `didSet` 都会被调用。

示例中的`willSet`使用了一个名为`newTotalSteps`的参数接收新值。在这个例子中只是简单的将新值输出。

`didSet`观察者会在`totalSteps`的值被修改后调用。它将`totalSteps`的新值与原值做比较，如果新值大于原值，则会输出新增了多少步。`didSet`观察者没有指定参数名，所以使用默认参数名`oldValue`。

> 注意

> 如果在`didSet`中给属性设置新值，那么新值会替换刚刚设置的值。


##全局变量和局部变量

上面关于属性的计算和观察功能对于全局变量和局部变量同样适用。全局变量定义在所有函数，方法，闭包，类型之外。局部变量定义在函数，方法或闭包内部。

在前面的章节中全局和局部变量都是存储变量，类似于存储属性，它为特定类型的值提供存储空间，并允许对其进行读写。

另外，还可以在全局或局部作用域中定义计算变量，或者为存储变量定义观察者。计算变量用来计算而非存储一个值，声明方式和计算属性一样。

> 注意
> 
> 和惰性存储属性的方式类似，全局常量和变量总是延迟计算的。不同的是，全局常量和变量不需要使用`@lazy`属性进行声明。
> 
> 局部常量和变量则绝不会延迟计算。


##类型属性

实例属性属于一个特定类型的实例。每次创建该类型的实例，它都拥有自己独立的一组属性，与其他实例对象无关。

还可以定义属于类型自身的属性。不论该类型有多少实例，这些属性都只有一份。这种属性被称为类型属性。

类型属性用于定义所有特定的类型实例都可以使用的值，比如所有实例都可以使用同一个常量属性（类似于`C`中的静态常量），或者就像所有的实例都可以使用全局变量属性（类似于`C`中的静态常量）。

对于值类型（结构和枚举），可以定义存储和计算类型的属性。对于类，则只能定义计算类型的属性。

值类型的存储类型属性可以是变量和常量。计算类型属性和计算实例属性相同，通常声明为变量属性。

> 注意
> 
> 与存储实例属性不同，必须为存储类型属性定义默认值。原因是类型本身没有一个可以在初始化时为类型属性赋值的构造器。


###类型属性语法

在`C`和`Objective-C`中，只能使用全局静态变量来定义依赖于某个属性的变量或常量。但在`Swift`中，类型属性可以作为类型定义的一部分，它的作用域也在类型的范围内。    

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
    

> 注意
>
> 上面的计算类型属性的示例都是只读的，仍然可以定义可读写的计算类型属性。


###查询和设置类型属性


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


下面的示例定义了一个结构体和两个类型属性来为声道音量建模。每一个声道的音量范围是0到10。

下图演示了如何将两个声道合并为一个立体声道。当某个声道的音量值是0时，所有灯都不会亮。当音量值是10时，所有灯都会亮起。下图中，左侧的音量值为9，右侧的音量值为7：

![Alt text](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/staticPropertiesVUMeter_2x.png)

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


`AudioChannel`定义了两个存储属性。首先，定义了音量最大值`thresholdLevel`，它是一个对所有实例可见的常量值。如果音量大于10，那么就取上限值10。

第二个类型属性是一个名为`maxInputLevelForAllChannels`的变量存储属性，用来表示所有实例的最大音量值。初始值为0。

`AudioChannel`结构体还定义了一个实例属性`currentLevel`，用来表示当前声道的音量值，取值0到10。

`currentLevel`的值在每次设置时都会通过`didSet`进行两种检查：

* 如果`currentLevel`的新值大于允许的最大值`thresholdLevel`，则属性监听器将`currentLevel`设置为`thresholdLevel`。
* 如果`currentLevel`的新值大于之前所有`AudioChannel`实例的值。那么属性监听器会将新值保存在静态属性`maxInputLevelForAllChannels`中。


> 注意
> 
> 在第一次检查过程中，`didSet`监听器将`currentLevel`设置为了不同的值，但此时不会再次调用属性监听器。

可以使用`AudioChannel`创建两个声道实例：`leftChannel`和`rightChannel`：

    var leftChannel = AudioChannel()
    var rightChannel = AudioChannel()
    
如果将`currentLevel`的左声道的值置为7，则可以看到类型属性`maxInputLevelForAllChannels`也更新为了7：

    leftChannel.currentLevel = 7
    println(leftChannel.currentLevel)
    // prints "7"
    // 输出 "7"
    println(AudioChannel.maxInputLevelForAllChannels)
    // print "7"
    // 输出 "7"

如果想将`currentLevel`的右声道设置为11，你会发现右声道的`currentLevel`值被设置为了10，同时`maxInputLevelForAllChannels` 也更新为10。


    rightChannel.currentLevel = 11
    println(rightChannel.currentLevel)
    // prints "10"
    // 输出 "10"
    println(AudioChannel.maxInputLevelForAllChannels)
    // prints "10"
    // 输出 "10"