# 方法 (Methods)

Methods are functions that are associated with a particular type. Classes, structures, and enumerations can all define instance methods, which encapsulate specific tasks and functionality for working with an instance of a given type. Classes, structures, and enumerations can also define type methods, which are associated with the type itself. Type methods are similar to class methods in Objective-C.

方法是指和某些特定类型相关联的函数。类、结构体、枚举都可以定义实例方法， 这些实例方法可以将特定任务和功能封装到一个指定的类型实例中。类、结构体、美剧也可以定义类型方法， 这些类型方法仅和类型本身有关联。 类型方法和 Objective-C 中的类方法(class methods)很相似。

The fact that structures and enumerations can define methods in Swift is a major difference from C and Objective-C. In Objective-C, classes are the only types that can define methods. In Swift, you can choose whether to define a class, structure, or enumeration, and still have the flexibility to define methods on the type you create.

事实上，结构体和枚举可以在 Swift 中定义方法， 成为了和 C、Objective-C 之间一个主要区别。在 Objective-C 中，只有类(Class)才能定义方法。在 Swift 中，你可以选择在类、结构体、枚举、甚至是你自己定义的类型中，去定义方法。

## 实例方法(Instance Methods)

Instance methods are functions that belong to instances of a particular class, structure, or enumeration. They support the functionality of those instances, either by providing ways to access and modify instance properties, or by providing functionality related to the instance’s purpose. Instance methods have exactly the same syntax as functions, as described in Functions.

实例方法是属于某个特定类、结构体、枚举实例的函数。实例方法提供获取和修改实例变量的途径，又或是提供与实例用途相关的功能，以满足这些实例的功能需要。实例方法的语法和函数一样，参考`函数`这一章节。

You write an instance method within the opening and closing braces of the type it belongs to. An instance method has implicit access to all other instance methods and properties of that type. An instance method can be called only on a specific instance of the type it belongs to. It cannot be called in isolation without an existing instance.

实例类型要写在类型的括号中。实例方法可以隐式地访问这个类型的所有实例方法和属性。实例方法只能被它所属类型的实例调用，不能在实例之外被独立调用。

Here’s an example that defines a simple `Counter` class, which can be used to count the number of times an action occurs:

这里有一个例子，定义了一个可以用来记录动作发生次数的计数器 Counter 类

```

class Counter {
    var count = 0
    func increment() {
        count++ 
    }
    func incrementBy(amount: Int) {
        count += amount
    }
    func reset() {
        count = 0
    }
}

```

The Counter class defines three instance methods:

`Counter` 类定义了三个实例方法：

* `increment` increments the counter by 1.

* `increment` * 计数器每次递增 +1。

* `incrementBy(amount: Int)` increments the counter by an specified integer amount.

* `incrementBy(amount: Int)` 计数器根据给定的 amount 值增量

* `reset` resets the counter to zero. 

* `reset` 重置计数器归零。

The `Counter` class also declares a variable property, count, to keep track of the current counter value.

`Counter` 类也声明了一个变量属性 count，用来记录当前的计数器的值。

You call instance methods with the same dot syntax as properties:

你可以像调用属性一样，通过相同的点语法 (dot syntax) 来调用实例方法：

```

let counter = Counter()
// the initial counter value is 0 
// 计数器初始值为0
counter.increment()
// the counter's value is now 1 
// 计数器的值现在是1
counter.incrementBy(5)
// the counter's value is now 6
// 计数器的值现在是6
counter.reset()
// the counter's value is now 0
// 计数器的值现在是0

```

## 方法的内部参数和外部参数（Local and External Parameter Names for Methods)

Function parameters can have both a local name (for use within the function’s body) and an external name (for use when calling the function), as described in External Parameter Names. The same is true for method parameters, because methods are just functions that are associated with a type. However, the default behavior of local names and external names is different for functions and methods.

函数参数可以有一个内部名称（用于函数内部）和一个外部名称（用于函数调用），正如`函数`章节里`外部参数名`描述的那样。方法参数和函数参数一样，因为方法只不过是和类型相关联的函数罢了。然而，内部名称和外部名称在函数和方法内部的默认行为却是不一样的。

Methods in Swift are very similar to their counterparts in Objective-C. As in Objective-C, the name of a method in Swift typically refers to the method’s first parameter using a preposition such as with, for, or by, as seen in the incrementBy method from the preceding Counter class example. The use of a preposition enables the method to be read as a sentence when it is called. Swift makes this established method naming convention easy to write by using a different default approach for method parameters than it uses for function parameters.

Swift 里的方法和 Objective-C 里的方法是非常相似的。和 Objective-C 中一样， Swift 里的方法通常使用 with、for、by 之类的介词来指向第一个参数，比如计数器例子里的 `incrementBy`。介词的使用可以使这个方法的调用如同阅读一个句子。与函数参数不同的是，对于方法参数，Swift 使用了一套不同的默认处理规则，使得方法的命名规则写起来更加简单。

Specifically, Swift gives the first parameter name in a method a local parameter name by default, and gives the second and subsequent parameter names both local and external parameter names by default. This convention matches the typical naming and calling convention you will be familiar with from writing Objective-C methods, and makes for expressive method calls without the need to qualify your parameter names.


具体来说，Swift 默认第一个参数名仅作为内部名称，第二个和之后的参数名作为内部名称和外部名称。这个约定和典型的命名和调用方法的约定相匹配，你会觉得和写 Objective-C 方法十分相似，而且这个约定不需要限制你的参数名。

Consider this alternative version of the Counter class, which defines a more complex form of the incrementBy method:

我们来看看计数器 `Counter` 的另外一个版本，这个版本定义了更加复杂的 `incrementBy` 方法：

```

class Counter {
    var count: Int = 0
    func incrementBy(amount: Int, numberOfTimes: Int) {
        count += amount * numberOfTimes
    }
}

```

This `incrementBy` method has two parameters—`amount` and `numberOfTimes`. By default, Swift treats `amount` as a local name only, but treats `numberOfTimes` as both a local and an external name. You call the method as follows:

这个 `incrementBy` 方法有两个参数 -- `amount` 和 `numberOfTimes`。根据默认约定，Swift 只把 `amount` 看做内部变量，但是把 `numberOfTimes` 同时作为内部名称和外部名称。你可以这样调用：

```

let counter = Counter()
counter.incrementBy(5, numberOfTimes: 3)
// counter value is now 15
// 计数器的值现在是15

```

You don’t need to define an external parameter name for the first argument value, because its purpose is clear from the function name `incrementBy`. The second argument, however, is qualified by an external parameter name to make its purpose clear when the method is called.

你不需要为第一个参数值定义一个外部参数名称，因为这个参数值的意图已经被函数名 `incrementBy` 表达得很清楚了。但是第二个参数被外部参数名限制了，这是为了在方法调用的时候，表达出更清晰的意图。

This default behavior effectively treats the method as if you had written a hash symbol (`#`) before the `numberOfTimes` parameter:

这种默认行为使方法处理变得高效，就好像你在 `numberOfTimes` 前加了一个 `#` 号：

```

func incrementBy(amount: Int, #numberOfTimes: Int) {
    count += amount * numberOfTimes
}

```

The default behavior described above mean that method definitions in Swift are written with the same grammatical style as Objective-C, and are called in a natural, expressive way.

以上描述的默认行为表，Swift 中的方法定义和 Objective-C 有着同样的语法风格，都使用了自然的表达手法。

## 修改方法的外部参数名称行为(Modifying External Parameter Name Behavior for Methods)

Sometimes it’s useful to provide an external parameter name for a method’s first parameter, even though this is not the default behavior. You can either add an explicit external name yourself, or you can prefix the first parameter’s name with a hash symbol to use the local name as an external name too.

有时候，提供为方法的第一个参数提供一个外部参数名称是有用的，即使这不是个默认行为。你可以自己增加一个明确的外部名称，也可以给第一个参数增加一个 # 的前缀，使得内部名称可以作为外部名称使用。

Conversely, if you do not want to provide an external name for the second or subsequent parameter of a method, override the default behavior by using an underscore character (`_`) as an explicit external parameter name for that parameter.

相反地，如果你不想为方法里的第二个及后续参数提供外部名称，可以使用 `_` 作为显式的外部参数名称来重写这个规则。

### The self Property

Every instance of a type has an implicit property called `self`, which is exactly equivalent to the instance itself. You use this implicit self property to refer to the current instance within its own instance methods.

每个类型的实例都有一个隐式的属性，叫做 `self`，这个变量和实例自身等价。你可以使用 self 来指代当前实例。

The `increment` method in the example above could have been written like this:

例子中的 `increment` 可以写成这样：

```

func increment() {
    self.count++
}

```

In practice, you don’t need to write `self` in your code very often. If you don’t explicitly write `self`, Swift assumes that you are referring to a property or method of the current instance whenever you use a known property or method name within a method. This assumption is demonstrated by the use of `count` (rather than `self.count`) inside the three instance methods for `Counter`.

事实上，你不需要经常在代码里写 `self`。如果你没有明确写 `self`，无论你调用了已知属性或是方法，Swift 会假设你调用的是当前实例的属性或者方法。这个假设已经在第一个例子里证实了， `Counter` 里直接调用了 `count` 而不是通过 `self.count`。

The main exception to this rule occurs when a parameter name for an instance method has the same name as a property of that instance. In this situation, the parameter name takes precedence, and it becomes necessary to refer to the property in a more qualified way. You use the implicit `self` property to distinguish between the parameter name and the property name.

当一个实例方法的参数名和这个实例里的属性名重复时，这个规则怎么处理呢？在这种情况下，参数名拥有更高的优先级，同时属性名的引用需要使用更清晰明确的方法。可以使用隐式的 `self` 来区分参数名和属性名。

Here, `self` disambiguates between a method parameter called `x` and an instance property that is also called `x`:

这里的 `self` 避免了方法参数名为 `x` 和实例属性名为 `x` 的混淆冲突：

```

struct Point {
    var x = 0.0, y = 0.0
    func isToTheRightOfX(x: Double) -> Bool {
        return self.x > x
    }
}
let somePoint = Point(x: 4.0, y: 5.0)
if somePoint.isToTheRightOfX(1.0) {
    println("This point is to the right of the line where x == 1.0")
}
// prints "This point is to the right of the line where x == 1.0

```

Without the `self` prefix, Swift would assume that both uses of `x` referred to the method parameter called `x`.

如果没有 `self` 这个前缀，Swift 会假设这两个 `x` 都指代参数 `x`。

### 修改实例方法中的值类型 (Modifying Value Types from Within Instance Methods)

Structures and enumerations are value types. By default, the properties of a value type cannot be modified from within its instance methods.

结构体和枚举都是值类型。值类型的属性默认不能在实例方法中被修改。

However, if you need to modify the properties of your structure or enumeration within a particular method, you can opt in to `mutating` behavior for that method. The method can then mutate (that is, change) its properties from within the method, and any changes that it makes are written back to the original structure when the method ends. The method can also assign a completely new instance to its implicit `self` property, and this new instance will replace the existing one when the method ends.

然而，如果你需要通过特殊方法来修改结构体或枚举的属性，你得为那个方法使用 `变异` 这个用法。这个方法可以在方法内部改变它的属性，并且在这个方法结束时，它产生的任何改变都会保留在原来的结构体实例中。方法也可以指定一个完整全新的实例替换隐式的 `self` 属性，从而在方法结束的时候，会替换原来的实例。

You can opt in to this behavior by placing the `mutating` keyword before the `func` keyword for that method:

你可以通过在 `func` 前增加 `mutating` 来调用 `变异` 

```

struct Point {
    var x = 0.0, y = 0.0
    mutating func moveByX(deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveByX(2.0, y: 3.0)
println("The point is now at (\(somePoint.x), \(somePoint.y))")
// prints "The point is now at (3.0, 4.0)

```

The `Point` structure above defines a mutating `moveByX` method, which moves a `Point` instance by a certain amount. Instead of returning a new point, this method actually modifies the point on which it is called. The `mutating` keyword is added to its definition to enable it to modify its properties.

上面这个 `Point` 结构体定义了一个变异的 `moveByX` 方法，这个方法可以将 `Point` 实例按照某个数值移动。这个方法在调用的时候修改了这个实例的坐标数据，而不是替换了这个实例。为了可以修改它的属性，在这个方法定义前增加了 `mutating` 。

Note that you cannot call a mutating method on a constant of structure type, because its properties cannot be changed, even if they are variable properties, as described in Stored Properties of Constant Structure Instances:

注意，你不能在一个作为常量的结构体实例上使用编译方法。因为它的属性已经无法更改，即使它们是可变属性。正如 `属性` 这个章节中的 `常量结构体实例的属性`中描述的那样。

```

let fixedPoint = Point(x: 3.0, y: 3.0)
fixedPoint.moveByX(2.0, y: 3.0)
// this will report an error
// 这里会报错

```

### 用变异方法给 self 赋值(Assigning to self Within a Mutating Method)

Mutating methods can assign an entirely new instance to the implicit `self` property. The `Point` example shown above could have been written in the following way instead:

变异方法可以将一个全新的实例赋值给 `self`。上面的 `Point` 例子可以被重写为如下： 

```

struct Point {
    var x = 0.0, y = 0.0
    mutating func moveByX(deltaX: Double, y deltaY: Double) {
        self = Point(x: x + deltaX, y: y + deltaY)
    }
}

```

This version of the mutating `moveByX` method creates a brand new structure whose `x` and `y` values are set to the target location. The end result of calling this alternative version of the method will be exactly the same as for calling the earlier version.

这个版本的变异 `moveByX` 重新创造了一个指向新坐标 `x` 和 `y` 的实例。调用这个版本的方法，执行结果和上一个版本相同。

Mutating methods for enumerations can set the implicit `self` parameter to be a different member from the same enumeration:

枚举类型的变异方法可以将 `self` 赋值为相同枚举类型中的另外一个成员。

```

enum TriStateSwitch {
    case Off, Low, High
    mutating func next() {
        switch self {
        case Off:
            self = Low
        case Low:
            self = High
        case High:
            self = Off
        }
    }
}
var ovenLight = TriStateSwitch.Low
ovenLight.next()
// ovenLight is now equal to .High
ovenLight.next()
// ovenLight is now equal to .Off

```

This example defines an enumeration for a three-state switch. The switch cycles between three different power states (`Off`, `Low` and `High`) every time its `next` method is called.

这个例子定义了一个有三种状态的枚举类型。每次调用 `next` 方法都会在这三种状态中切换一次。

## 类型方法 (Type Methods)

Instance methods, as described above, are methods that are called on an instance of a particular type. You can also define methods that are called on the type itself. These kinds of methods are called type methods. You indicate type methods for classes by writing the keyword `class` before the method’s `func` keyword, and type methods for structures and enumerations by writing the keyword `static` before the method’s `func` keyword.

上面描述的实例方法，都是在一个指定类型的实例中调用的。你也可以定义可以被类型自身调用的方法。这些类型的方法被称为类型方法。在类中，你可以通过在 `func` 关键词前增加 `class` 前缀来指定这个方法为类型方法。在结构体和枚举中，你可以通过在 `func` 关键词前增加 `static` 前缀来指定这个方法为类型方法

> NOTE 提示 

> In Objective-C, you can define type-level methods only for Objective-C classes. In Swift, you can define type-level methods for all classes, structures, and enumerations. Each type method is explicitly scoped to the type it supports.

> 在 Objective-C 中，你可以给 Objective-C 类指定一个类型级别的方法。在 Swift 中，你可以为所有类、结构体、枚举指定类型级别的方法。每个类型方法仅显式包含在它支持的类中

Type methods are called with dot syntax, like instance methods. However, you call type methods on the type, not on an instance of that type. Here’s how you call a type method on a class called `SomeClass`:

和实例方法一样，类型方法也通过点语法 (dot syntax) 被调用。然后你可以直接在类型上调用这个方法，而不是在一个类型的实例上。下面的 `SomeClass` 会表明如何调用类型方法：

```

class SomeClass {
    class func someTypeMethod() {
        // type method implementation goes here
    }
}
SomeClass.someTypeMethod()

```

Within the body of a type method, the implicit self property refers to the type itself, rather than an instance of that type. For structures and enumerations, this means that you can use self to disambiguate between static properties and static method parameters, just as you do for instance properties and instance method parameters.

在类型方法体中，隐式 self 属性指代类型本身，而不是某个类型的实例。对于结构体和枚举来说，这意味着你可以使用 self 来解除静态属性和静态方法参数之间的混淆，就如同实例属性和实例方法参数那样。

More generally, any unqualified method and property names that you use within the body of a type method will refer to other type-level methods and properties. A type method can call another type method with the other method’s name, without needing to prefix it with the type name. Similarly, type methods on structures and enumerations can access static properties by using the static property’s name without a type name prefix.

更广泛的说，在类型方法体内，没有显式调用的方法和属性都会被指代为其他类型级别的方法和属性。类型方法可以通过其他方法名来调用其他类型方法，而不需要在方法名前增加类型名称。同样的，结构体和枚举的类型方法也可以通过静态属性名直接获取静态属性，而不需要在属性名前增加类型名称。

The example below defines a structure called `LevelTracker`, which tracks a player’s progress through the different levels or stages of a game. It is a single-player game, but can store information for multiple players on a single device.

下面这个例子指定了 `LevelTracker` 结构体。它可以跟踪一个游戏中成员的不同关卡过程。这是一个单玩家游戏，但是可以在单个设备中存储多个玩家的游戏数据。

All of the game’s levels (apart from level one) are locked when the game is first played. Every time a player finishes a level, that level is unlocked for all players on the device. The `LevelTracker` structure uses static properties and methods to keep track of which levels of the game have been unlocked. It also tracks the current level for an individual player.

游戏刚开始的时候，所有游戏关卡（除了第一关）都被锁定。每次一个玩家结束了一个关卡，这个关卡会为这个设备上的所有玩家解锁。`LevelTracker` 结构体使用了静态属性和方法来记录哪个游戏关卡被解锁，同时记录为每个成员玩家当前所在关卡。

```

struct LevelTracker {
    static var highestUnlockedLevel = 1
    static func unlockLevel(level: Int) {
        if level > highestUnlockedLevel { highestUnlockedLevel = level }
    }
    static func levelIsUnlocked(level: Int) -> Bool {
        return level <= highestUnlockedLevel
    }
    var currentLevel = 1
    mutating func advanceToLevel(level: Int) -> Bool {
        if LevelTracker.levelIsUnlocked(level) {
            currentLevel = level
            return true
        } else {
            return false
        }
    }
}

```

The `LevelTracker` structure keeps track of the highest level that any player has unlocked. This value is stored in a static property called `highestUnlockedLevel`.

`LevelTracker` 结构体持续记录被任何一个玩家解锁的最高关卡。这个值被保存在静态属性 `highestUnlockedLevel` 中。

`LevelTracker` also defines two type functions to work with the `highestUnlockedLevel` property. The first is a type function called `unlockLevel`, which updates the value of `highestUnlockedLevel` whenever a new level is unlocked. The second is a convenience type function called `levelIsUnlocked`, which returns `true` if a particular level number is already unlocked. (Note that these type methods can access the `highestUnlockedLevel` static property without your needing to write it as `LevelTracker.highestUnlockedLevel`.)

`LevelTracker` 也指定了两个与 `highestUnlockedLevel` 一起工作的类型函数。第一个类型函数 `unlockLevel` ，当新关卡解锁时，用来更新 `highestUnlockedLevel` 。第二个是 `levelIsUnlocked`，如果某个关卡编号已经解锁，返回 `true`。（注意，这些类型方法在获取 `highestUnlockedLevel` 属性时，不需要写成 `LevelTracker.highestUnlockedLevel` 也能直接获取 `highestUnlockedLevel` 这个静态属性。）

In addition to its static property and type methods, `LevelTracker` tracks an individual player’s progress through the game. It uses an instance property called `currentLevel` to track the level that a player is currently playing.

除了静态属性和类型方法之外，`LevelTracker` 也跟踪每个独立玩家在游戏中的进程。通过一个实例属性 `currentLevel` 来记录玩家当前的关卡。

To help manage the `currentLevel` property, `LevelTracker` defines an instance method called `advanceToLevel`. Before updating `currentLevel`, this method checks whether the requested new level is already unlocked. The `advanceToLevel` method returns a Boolean value to indicate whether or not it was actually able to set `currentLevel`.

为了帮助管理 `currentLevel` 属性，`LevelTracker` 指定了一个实例方法 `advanceToLevel`。在更新 `currentLevel` 之前，这个方法会检测请求的下一关已经解锁。`advanceToLevel` 方法返回一个布尔值，表示是否可以前进到某个关卡。

The `LevelTracker` structure is used with the `Player` class, shown below, to track and update the progress of an individual player:

`LevelTracker` 结构体可以和 `Player` 类结合使用，来跟踪和更新每个玩家的游戏进程：

```

class Player {
    var tracker = LevelTracker()
    let playerName: String
    func completedLevel(level: Int) {
        LevelTracker.unlockLevel(level + 1)
        tracker.advanceToLevel(level + 1)
    }
    init(name: String) {
        playerName = name
    }
}

```

The `Player` class creates a new instance of `LevelTracker` to track that player’s progress. It also provides a method called `completedLevel`, which is called whenever a player completes a particular level. This method unlocks the next level for all players and updates the player’s progress to move them to the next level. (The Boolean return value of `advanceToLevel` is ignored, because the level is known to have been unlocked by the call to `LevelTracker.unlockLevel` on the previous line.)

`Player` 实例化了一个 `LevelTracker` 来追踪玩家的游戏进程。它也提供了 `completedLevel` 方法，当一个玩家完成某个特定关卡时将会被调用。这个方法为所有玩家解锁下一个关卡，并且更新玩家的进程到下一个关卡。（`advanceToLevel` 的布尔返回值被忽略了， 因为 `LevelTracker.unlockLevel` 已经在这个方法之前解锁了下一个关。）

You can create a instance of the `Player` class for a new player, and see what happens when the player completes level one:

你可以为一个新玩家实例化一个 `Player` 类，然后看看当玩家完成第一关的时候会发生什么：

```

var player = Player(name: "Argyrios")
player.completedLevel(1)
println("highest unlocked level is now \(LevelTracker.highestUnlockedLevel)")
// prints "highest unlocked level is now 2

```

If you create a second player, whom you try to move to a level that is not yet unlocked by any player in the game, the attempt to set the player’s current level fails:

如果你实例化了第二个玩家，并试图让他进入一个尚未解锁的关卡，这会导致失败：

```

player = Player(name: "Beto")
if player.tracker.advanceToLevel(6) {
    println("player is now on level 6")
} else {
    println("level 6 has not yet been unlocked")
}
// prints "level 6 has not yet been unlocked

```