#Protocols
A protocol defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol doesn’t actually provide an implementation for any of these requirements—it only describes what an implementation will look like. The protocol can then be adopted by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to conform to that protocol.


#协议

一个协议(protocol)定义了适合特定的任务或功能的方法、属性和其他需求。协议并不提供这些需求的实现，只描述了这个实现应该是怎样的。

协议能够被类(class)，结构体(structure),枚举(enumeration)适配(adopted)，同时，这些类型如果了满足一个协议需求，则被称为遵循(conform to)协议

Protocols can require that conforming types have specific instance properties, instance methods, type methods, operators, and subscripts.

协议可以要求遵循(conforming)的类型有特定的实例属性(instance properties),实例方法(instance methods),类型方法(type methods),操作符(operators)和下标(subscripts)。


##Protocol Syntax
##协议语法
You define protocols in a very similar way to classes, structures, and enumerations:

定义协议，与定义类，结构体，枚举的方式非常相似，如下所示：

    protocol SomeProtocol {
        // protocol definition goes here
    }
    
Custom types state that they adopt a particular protocol by placing the protocol’s name after the type’s name, separated by a colon, as part of their definition. Multiple protocols can be listed, and are separated by commas:

在类型名称后添加协议名称，并以冒号`:`分割，表示自定义类型(Custom types)适配一个特定协议；实现多个协议时，各协议之间用逗号`,`分隔,如下所示：

    struct SomeStructure: FirstProtocol, AnotherProtocol {
        // structure definition goes here
    }
If a class has a superclass, list the superclass name before any protocols it adopts, followed by a comma:

若某个类有父类，要把父类放在所有其适配的协议之前，且用逗号`,`分割,如下所示：

    class SomeClass: SomeSuperclass, FirstProtocol, AnotherProtocol {
        // class definition goes here
    }
    
Property Requirements

##属性要求

A protocol can require any conforming type to provide an instance property or type property with a particular name and type. The protocol doesn’t specify whether the property should be a stored property or a computed property—it only specifies the required property name and type. The protocol also specifies whether each property must be gettable or gettable and settable.

协议可以要求任何遵循(conforming)类型，提供一个特定名称和类型的实例属性(instance property)或类型属性（type property）。协议不指定属性是存储型属性(stored property)还是计算型属性(calculate property)。
协议同时指定了每个属性是否是可读(gettable)或可读写(gettable and settable)


If a protocol requires a property to be gettable and settable, that property requirement cannot be fulfilled by a constant stored property or a read-only computed property. If the protocol only requires a property to be gettable, the requirement can be satisfied by any kind of property, and it is valid for it also to be settable if this is useful for your own code.

如果协议要求属性可读写(gettable and settable)，那常量存储属性（constant stored property）或者只读计算属性（read-only computed property）都无法满足此要求。如果协议只要求属性可读(gettable)，那任何类型的属性都满足这个要求，即使这些属性是可写(settable)的。

Property requirements are always declared as variable properties, prefixed with the var keyword. Gettable and settable properties are indicated by writing { get set } after their type declaration, and gettable properties are indicated by writing { get }.

协议里的属性要求，通常都是通过使用`var`关键字来声明的变量属性。
在类型声明之后用{ get set }表示属性为可读写的。{ get }表示属性为可读的。

    protocol SomeProtocol {
        var mustBeSettable: Int { get set }
        var doesNotNeedToBeSettable: Int { get }
    }
    
Always prefix type property requirements with the class keyword when you define them in a protocol. This is true even though type property requirements are prefixed with the static keyword when implemented by a structure or enumeration:

当你在一个协议中定义一个某种类型的属性要求，总要前置`class` 关键字。同样某类型属性要求使用`static`关键字前缀,来定义结构体(structure)或枚举类型(enumeration)

> 这样翻译正确么？

    protocol AnotherProtocol {
        class var someTypeProperty: Int { get set }
    }
    
Here’s an example of a protocol with a single instance property requirement:

下面是协议的一个例子,这个协议只有一个实例属性(instance property)要求:


    protocol FullyNamed {
        var fullName: String { get }
    }
    
The FullyNamed protocol defines any kind of thing that has a fully-qualified name. It doesn’t specify what kind of thing it must be—it only specifies that the thing must be able to provide a full name for itself. It specifies this requirement by stating that any FullyNamed type must have a gettable instance property called fullName, which is of type String.

`FullyNamed`协议可以定义任何需要一个完整`name`的类型(方法，属性或者其他需求)。这个协议并不指定什么，只有一个需求：这个类型本身必须提供一个完整的名称。这个需求通过声明一个`String`类型的实例属性`fullName`,且这个属性必须是可读的(gettable)来指定。



Here’s an example of a simple structure that adopts and conforms to the FullyNamed protocol:

下面的例子中，一个简单的结构体适配且遵循`FullyNamed`协议

    struct Person: FullyNamed {
        var fullName: String
    }
    let john = Person(fullName: "John Appleseed")
    // john.fullName is "John Appleseed"

This example defines a structure called Person, which represents a specific named person. It states that it adopts the FullyNamed protocol as part of the first line of its definition.

这个例子中定义了一个名为`Person`的结构体，代表一个有名字的人。它在第一行的结构体定义中，声明了其适配`FullyNamed`协议。

Each instance of Person has a single stored property called fullName, which is of type String. This matches the single requirement of the FullyNamed protocol, and means that Person has correctly conformed to the protocol. (Swift reports an error at compile-time if a protocol requirement is not fulfilled.)

每个`Person`实例都有一个单独存储的，`String`类型的属性`fullName`。拥有这个属性代表满足了`FullyNamed`协议的要求,这意味着`Person`遵循协议。(在编译时如果不满足协议要求，swift会报告一个错误)。


Here’s a more complex class, which also adopts and conforms to the FullyNamed protocol:
下面有一个更复杂的类,同样适配且遵循`FullyNamed`协议

    class Starship: FullyNamed {
        var prefix: String?
        var name: String
        init(name: String, prefix: String? = nil) {
            self.name = name
            self.prefix = prefix
        }
        var fullName: String {
        return (prefix ? prefix! + " " : "") + name
        }
    }
    var ncc1701 = Starship(name: "Enterprise", prefix: "USS")
    // ncc1701.fullName is "USS Enterprise"
    
This class implements the fullName property requirement as a computed read-only property for a starship. Each Starship class instance stores a mandatory name and an optional prefix. The fullName property uses the prefix value if it exists, and prepends it to the beginning of name to create a full name for the starship.
这个类提供了`fullName`属性，这个属性是`starship`这个类的一个只读的计算属性。
每个`starship`类的实例存储一个强制性的名称和一个可选的前缀。当存在前缀时，`fullName`属性会把前缀添加到名称前面,从而创建了一个`starship`的全名。


Method Requirements

Protocols can require specific instance methods and type methods to be implemented by conforming types. These methods are written as part of the protocol’s definition in exactly the same way as for normal instance and type methods, but without curly braces or a method body. Variadic parameters are allowed, subject to the same rules as for normal methods.



方法需求

若某种类型遵循协议，协议可以要求指定特定的实例方法和类型方法。这些方法作为协议定义的一部分，跟通常定义实例与类型方法的途径完全一样,但不需要书写大括号或方法的主体。方法允许含有可变参数,且与通常的方法遵循同样的规则。

NOTE

Protocols use the same syntax as normal methods, but are not allowed to specify default values for method parameters.

注意

协议与通常的方法语法相同，但不允许指定方法中参数的默认值

As with type property requirements, you always prefix type method requirements with the class keyword when they are defined in a protocol. This is true even though type method requirements are prefixed with the static keyword when implemented by a structure or enumeration:

    protocol SomeProtocol {
        class func someTypeMethod()
    }
    
当你在一个协议中定义一个某种类型的方法要求，要前置`class` 关键字。同样某类型方法要求使用`static`关键字前缀,来定义结构体(structure)或枚举类型(enumeration)

The following example defines a protocol with a single instance method requirement:
下面的例子中，定义了一个协议，协议要求一个实例方法。

    protocol RandomNumberGenerator {
        func random() -> Double
    }
This protocol, RandomNumberGenerator, requires any conforming type to have an instance method called random, which returns a Double value whenever it is called. (Although it is not specified as part of the protocol, it is assumed that this value will be a number between 0.0 and 1.0 inclusive.)

`RandomNumberGenerator`,该协议要求任何遵循协议的类型调用一个名为random的实例方法,这个方法无论何时调用，都会返回一个Double类型的值。(这个值在0.0与1.0之间，这一点没有在协议中指出)。


The RandomNumberGenerator protocol does not make any assumptions about how each random number will be generated—it simply requires the generator to provide a standard way to generate a new random number.

Here’s an implementation of a class that adopts and conforms to the RandomNumberGenerator protocol. This class implements a pseudorandom number generator algorithm known as a linear congruential generator:

　`RandomNumberGenerator`协议不会描述如何建立一个随机数，只需要指定一个随机数生成器，从而提供一种标准的方式来生成一个新随机数。
　　
　下面是一个类的实现,遵循`RandomNumberGenerator`协议。这个类实现了一种伪随机数发生器算法，称为线性同余（linear congruential）发生器:


    class LinearCongruentialGenerator: RandomNumberGenerator {
        var lastRandom = 42.0
        let m = 139968.0
        let a = 3877.0
        let c = 29573.0
        func random() -> Double {
            lastRandom = ((lastRandom * a + c) % m)
            return lastRandom / m
        }
    }
    let generator = LinearCongruentialGenerator()
    println("Here's a random number: \(generator.random())")
    // prints "Here's a random number: 0.37464991998171"
    println("And another one: \(generator.random())")
    // prints "And another one: 0.729023776863283"

Mutating Method Requirements

突变方法要求

It is sometimes necessary for a method to modify (or mutate) the instance it belongs to. For instance methods on value types (that is, structures and enumerations) you place the mutating keyword before a method’s func keyword to indicate that the method is allowed to modify the instance it belongs to and/or any properties of that instance. This process is described in Modifying Value Types from Within Instance Methods.

有时，实例的一个方法需要修改（或突变）实例的类型。对值类型（value types）(即结构体和枚举类型)的实例方法中，使用`mutating`关键字,写在方法的函数关键字`fun`前面，来表明实例中该方法允许修改其类型及任何属性。这个过程在 `在实例方法中修改值类型`章节中有详细的描述。

If you define a protocol instance method requirement that is intended to mutate instances of any type that adopts the protocol, mark the method with the mutating keyword as part of the protocol’s definition. This enables structures and enumerations to adopt the protocol and satisfy that method requirement.

如果你定义的协议中，某个实例适配此协议，而实例方法需要改变其类型，协议定义时要在此方法前加上关键字`mutating`。这样可以让结构体及枚举类型适配协议，且满足实例方法的需求。

NOTE
注意

If you mark a protocol instance method requirement as mutating, you do not need to write the mutating keyword when writing an implementation of that method for a class. The mutating keyword is only used by structures and enumerations.


如果你在一个协议中实现的突变方法是为一个类服务的，不需要为其加`上mutating`关键字。
mutating`关键字只用在结构体与枚举类型中。
`

The example below defines a protocol called Togglable, which defines a single instance method requirement called toggle. As its name suggests, the toggle method is intended to toggle or invert the state of any conforming type, typically by modifying a property of that type.

下面的例子中定义了一个`togglable`协议，包含一个名为`togger`的突变实例方法。正如名称所表达的，适配此协议的某实例中，toggle方法通常会通过改变实例的某个属性，来切换或恢复其类型。

The toggle method is marked with the mutating keyword as part of the Togglable protocol definition, to indicate that the method is expected to mutate the state of a conforming instance when it is called:

`toggle`方法前面加上了`mutating`关键字，作为`Togglabel`协议定义的一部分，则表示一个适配`toggleabel`协议的实例中，这个方法会在调用时改变实例的类型。

    protocol Togglable {
        mutating func toggle()
    }
    
If you implement the Togglable protocol for a structure or enumeration, that structure or enumeration can conform to the protocol by providing an implementation of the toggle method that is also marked as mutating.

当你提供的枚举或结构体遵循`Togglable`协议时，需要提供一个带有`mutating`前缀的`toggle`方法。


The example below defines an enumeration called OnOffSwitch. This enumeration toggles between two states, indicated by the enumeration cases On and Off. The enumeration’s toggle implementation is marked as mutating, to match the Togglable protocol’s requirements:

    enum OnOffSwitch: Togglable {
        case Off, On
        mutating func toggle() {
            switch self {
            case Off:
                self = On
            case On:
                self = Off
            }
        }
    }
    var lightSwitch = OnOffSwitch.Off
    lightSwitch.toggle()
    // lightSwitch is now equal to .On
    
Protocols as Types

协议类型

Protocols do not actually implement any functionality themselves. Nonetheless, any protocol you create will become a fully-fledged type for use in your code.

尽管协议本身并不实现任何功能，但协议可以作为完整的类型来使用。

Because it is a type, you can use a protocol in many places where other types are allowed, including:

你可以把协议类型用在其他类型适用的场景里，比如：

As a parameter type or return type in a function, method, or initializer

在函数，方法或构造方法中作为形参类型（parameter type）或返回值类型（return type）

As the type of a constant, variable, or property

作为常量、变量或属性这三种类型之一

As the type of items in an array, dictionary, or other container

作为数组，字典或其他容器中的元素类型

NOTE
注意

Because protocols are types, begin their names with a capital letter (such as FullyNamed and RandomNumberGenerator) to match the names of other types in Swift (such as Int, String, and Double).

注意: 协议是一种类型，因此协议类型的名称应与Swift中其他类型(Int，Double，String)的写法相同，每一个单字的首字母都采用大写字母（大驼峰写法）

Here’s an example of a protocol used as a type:

下面的例子中，协议被当作类型使用：

    class Dice {
        let sides: Int
        let generator: RandomNumberGenerator
        init(sides: Int, generator: RandomNumberGenerator) {
            self.sides = sides
            self.generator = generator
        }
        func roll() -> Int {
            return Int(generator.random() * Double(sides)) + 1
        }
    }
    
This example defines a new class called Dice, which represents an n-sided dice for use in a board game. Dice instances have an integer property called sides, which represents how many sides they have, and a property called generator, which provides a random number generator from which to create dice roll values.

例子中定义了一个`Dice`类，用来表示桌游中的拥有N个面的骰子。`Dice`的实例包含`sides`和`generator`两个属性，前者是整型（integer），用来表示骰子有几个面，后者提供了一个随机数生成器，来表示骰子掷出的值。

The generator property is of type RandomNumberGenerator. Therefore, you can set it to an instance of any type that adopts the RandomNumberGenerator protocol. Nothing else is required of the instance you assign to this property, except that the instance must adopt the RandomNumberGenerator protocol.

`generator`属性的类型为`RandomNumberGenerator`，因此任何类型，若适配`RandomNumberGenerator`协议，其实例都可以赋值给`generator`，除此以外没有其他要求。

Dice also has an initializer, to set up its initial state. This initializer has a parameter called generator, which is also of type RandomNumberGenerator. You can pass a value of any conforming type in to this parameter when initializing a new Dice instance.

`Dice`类也包含一个构造方法，用于设置其初始状态。这个方法包含一个同样是`RandomNumberGenerator`类型的参数`generator`。在构造一个新的`Dice`的实例时，可以传入任何遵循`RandomNumberGenerator`协议的类型作为`generator`

Dice provides one instance method, roll, which returns an integer value between 1 and the number of sides on the dice. This method calls the generator’s random method to create a new random number between 0.0 and 1.0, and uses this random number to create a dice roll value within the correct range. Because generator is known to adopt RandomNumberGenerator, it is guaranteed to have a random method to call.

Dice类提供了一个实例方法`roll`,此方法会返回一个整型值，介于1和骰子面的数量之间。这个方法调用`generator`的随机数方法,来创建一在0.0和1.0之间的随机数,并使用这个随机数来确保骰子的滚动值在正确的范围内。因为`generator`适配`RandomNumberGenerator`协议,因此它可以保证有一个`random`方法供调用。

Here’s how the Dice class can be used to create a six-sided dice with a LinearCongruentialGenerator instance as its random number generator:

下面的例子中，展示了如何使用线性同余发生器（LinearCongruentialGenerator）的实例作为随机数生成器，从而创建一个六面的骰子:    
    

    var d6 = Dice(sides: 6, generator: LinearCongruentialGenerator())
    for _ in 1...5 {
        println("Random dice roll is \(d6.roll())")
    }
    // Random dice roll is 3
    // Random dice roll is 5
    // Random dice roll is 4
    // Random dice roll is 5
    // Random dice roll is 4
    
Delegation
代理

Delegation is a design pattern that enables a class or structure to hand off (or delegate) some of its responsibilities to an instance of another type. This design pattern is implemented by defining a protocol that encapsulates the delegated responsibilities, such that a conforming type (known as a delegate) is guaranteed to provide the functionality that has been delegated. Delegation can be used to respond to a particular action, or to retrieve data from an external source without needing to know the underlying type of that source.

代理（Delegation）是一种设计模式，它允许类或结构体将一些他们负责的功能转交(代理)给其他类型的实例。
委托模式的实现需要定义一个协议，这个协议封装了那些需要被代理的功能，而一个遵循此协议的实例则拥有这些功能

The example below defines two protocols for use with dice-based board games:

下面的例子中定义了两个基于骰子游戏的协议：

    protocol DiceGame {
        var dice: Dice { get }
        func play()
    }
    protocol DiceGameDelegate {
        func gameDidStart(game: DiceGame)
        func game(game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int)
        func gameDidEnd(game: DiceGame)
    }
    
The DiceGame protocol is a protocol that can be adopted by any game that involves dice. The DiceGameDelegate protocol can be adopted by any type to track the progress of a DiceGame.

`DiceGame`协议可以被任意含有骰子的游戏所适配，`DiceGameDelegate`协议可以被任意用来追踪`DiceGame`过程的类型所适配

Here’s a version of the Snakes and Ladders game originally introduced in Control Flow. This version is adapted to use a Dice instance for its dice-rolls; to adopt the DiceGame protocol; and to notify a DiceGameDelegate about its progress:

这里有一个，`Snakes and Ladders`游戏的新版本（之前的版本在流程控制这一节中介绍过）。新版本使用`Dice`类的实例作为掷骰子的需求，并且适配了`DiceGame`协议。同时通知(notify)`DiceGameDelegate`协议，用来记录游戏过程:

    class SnakesAndLadders: DiceGame {
        let finalSquare = 25
        let dice = Dice(sides: 6, generator: LinearCongruentialGenerator())
        var square = 0
        var board: Int[]
        init() {
            board = Int[](count: finalSquare + 1, repeatedValue: 0)
            board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
            board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
        }
        var delegate: DiceGameDelegate?
        func play() {
            square = 0
            delegate?.gameDidStart(self)
            gameLoop: while square != finalSquare {
                let diceRoll = dice.roll()
                delegate?.game(self, didStartNewTurnWithDiceRoll: diceRoll)
                switch square + diceRoll {
                case finalSquare:
                    break gameLoop
                case let newSquare where newSquare > finalSquare:
                    continue gameLoop
                default:
                    square += diceRoll
                    square += board[square]
                }
            }
            delegate?.gameDidEnd(self)
        }
    }
For a description of the Snakes and Ladders gameplay, see the Break section of the Control Flow chapter.

你可以参考流程控制章节中对此游戏的介绍

> 译者注 Snakes and Ladders 是蛇梯棋游戏，一种类似大富翁的游戏。

This version of the game is wrapped up as a class called SnakesAndLadders, which adopts the DiceGame protocol. It provides a gettable dice property and a play method in order to conform to the protocol. (The dice property is declared as a constant property because it does not need to change after initialization, and the protocol only requires that it is gettable.)

这个版本的游戏封装为`SnakesAndLadders`类，该类适配`DiceGame`协议。这个类还提供了可读的`dice`属性和`play`方法，从而遵循了`DiceGame`协议。(`dice`属性声明为常量，因为构造之后dice属性就不在改变，且协议只要求`dice`为只读)



The Snakes and Ladders game board setup takes place within the class’s init() initializer. All game logic is moved into the protocol’s play method, which uses the protocol’s required dice property to provide its dice roll values.

`Snakes And Ladders`游戏通过构造方法(initializer)`init`初始化游戏。所有的游戏逻辑移到了`play`方法中，`play`方法使用协议要求的`dice`属性，来提供骰子掷出的值。

Note that the delegate property is defined as an optional DiceGameDelegate, because a delegate isn’t required in order to play the game. Because it is of an optional type, the delegate property is automatically set to an initial value of nil. Thereafter, the game instantiator has the option to set the property to a suitable delegate.

注意，`delegate`属性并不是游戏运行所必须的，因此`delegate`被定义为`DiceGameDelegate`协议类型的可选属性，`delegate`使用nil作为初始值。此后,游戏实例可以选择将其设置为一个合适的代理。



DiceGameDelegate provides three methods for tracking the progress of a game. These three methods have been incorporated into the game logic within the play method above, and are called when a new game starts, a new turn begins, or the game ends.

`DicegameDelegate`协议提供了三个方法来跟踪游戏过程。这三个方法存在于游戏的逻辑中，即上面的play()方法内。分别在游戏开始时，新一轮开始时，游戏结束时被调用。


Because the delegate property is an optional DiceGameDelegate, the play method uses optional chaining each time it calls a method on the delegate. If the delegate property is nil, these delegate calls fail gracefully and without error. If the delegate property is non-nil, the delegate methods are called, and are passed the SnakesAndLadders instance as a parameter.

因为`delegate`属性是一个遵循`DiceGameDelegate`的可选属性，因此在`play`方法中使用了可选链（optional chaining ）来在代理时调用方法。 若`delegate`属性为`nil`， 则`delegate`所调用的方法正常失败（fail gracefully）且不报错。若`delegate`不为`nil`，则方法能够被调用，且作为一个参数传入`SnakesAndLadders`实例中

This next example shows a class called DiceGameTracker, which adopts the DiceGameDelegate protocol:

下一个例子展示了一个名为`DiceGameTracker`的类，适配`DiceGameDelegate`协议。

    class DiceGameTracker: DiceGameDelegate {
        var numberOfTurns = 0
        func gameDidStart(game: DiceGame) {
            numberOfTurns = 0
            if game is SnakesAndLadders {
                println("Started a new game of Snakes and Ladders")
            }
            println("The game is using a \(game.dice.sides)-sided dice")
        }
        func game(game: DiceGame, didStartNewTurnWithDiceRoll diceRoll: Int) {
            ++numberOfTurns
            println("Rolled a \(diceRoll)")
        }
        func gameDidEnd(game: DiceGame) {
            println("The game lasted for \(numberOfTurns) turns")
        }
    }
    
DiceGameTracker implements all three methods required by DiceGameDelegate. It uses these methods to keep track of the number of turns a game has taken. It resets a numberOfTurns property to zero when the game starts; increments it each time a new turn begins; and prints out the total number of turns once the game has ended.

DiceGameTracker提供了DiceGameDelegate所要求的三个方法。它使用这三个方法来跟踪游戏进行的轮数。当游戏开始时，将numberOfTurns属性重置为0。每轮开始后递增这个值。当游戏结束时打印游戏进行的总轮数

The implementation of gameDidStart shown above uses the game parameter to print some introductory information about the game that is about to be played. The game parameter has a type of DiceGame, not SnakesAndLadders, and so gameDidStart can access and use only methods and properties that are implemented as part of the DiceGame protocol. However, the method is still able to use type casting to query the type of the underlying instance. In this example, it checks whether game is actually an instance of SnakesAndLadders behind the scenes, and prints an appropriate message if so.

在如上所示的gameDidStart方法的实现中，游戏即将开始时使用了game参数来打印一些介绍性信息。game参数拥有一个DiceGame类型,而不是SnakesAndLadders,所以gameDidStart方法只能访问和使用DiceGame协议中的方法和属性。然而,该方法仍然能够使用类型检查（type casting）查询底层实例的类型。在这个例子中,它在幕后检查游戏是否是SnakesAndLadders的一个实例,当确认后打印一个适当的消息。

gameDidStart also accesses the dice property of the passed game parameter. Because game is known to conform to the DiceGame protocol, it is guaranteed to have a dice property, and so the gameDidStart method is able to access and print the dice’s sides property, regardless of what kind of game is being played.

gameDidStart方法也能够访问dice属性，这个属性存在于被传递为参数的game中。game遵循DiceGame协议，因此被赋予了dice属性，不管运行何种游戏，gameDidStart方法都可以访问且打印骰子的边数。


下面是DiceGameTracker的运行过程：
Here’s how DiceGameTracker looks in action:

    let tracker = DiceGameTracker()
    let game = SnakesAndLadders()
    game.delegate = tracker
    game.play()
    // Started a new game of Snakes and Ladders
    // The game is using a 6-sided dice
    // Rolled a 3
    // Rolled a 5
    // Rolled a 4
    // Rolled a 5
    // The game lasted for 4 turns

Adding Protocol Conformance with an Extension

使用扩展添加协议一致性

You can extend an existing type to adopt and conform to a new protocol, even if you do not have access to the source code for the existing type. Extensions can add new properties, methods, and subscripts to an existing type, and are therefore able to add any requirements that a protocol may demand. For more about extensions, see Extensions.

即便不能修改现有类型的代码，你也可以扩展现有类型，从而适配和遵循新协议。扩展（extensions）可以在现有的类型上添加新属性、方法和下标,因此能够满足任何一个协议的需要。更多关于扩展相关的内容，请参考扩展。

NOTE
注意

Existing instances of a type automatically adopt and conform to a protocol when that conformance is added to the instance’s type in an extension.

当你使用一个扩展，为一个实例的类型添加上某种对协议的适配后，这个类型已存在的所有实例，都会自动适配与遵循此协议。

For example, this protocol, called TextRepresentable, can be implemented by any type that has a way to be represented as text. This might be a description of itself, or a text version of its current state:

举例来讲，下面的TextRepersentable协议，可以被任何能表现为文字的类型所适配。这有可能是其自身的描述，或是其状态的文字版本。

    protocol TextRepresentable {
        func asText() -> String
    }
    
The Dice class from earlier can be extended to adopt and conform to TextRepresentable:

之前的Dice类可以扩展为适配并遵循TextRepresentable协议：
    
    extension Dice: TextRepresentable {
        func asText() -> String {
            return "A \(sides)-sided dice"
        }
    }
    
This extension adopts the new protocol in exactly the same way as if Dice had provided it in its original implementation. The protocol name is provided after the type name, separated by a colon, and an implementation of all requirements of the protocol is provided within the extension’s curly braces.

这个扩展以完全相同的方式适配了新协议，就像骰子提供了最初（适配协议）的实现。协议名称放在类型名称后,用`:`隔开,协议所要求的实现则提供在扩展的花括号内。


Any Dice instance can now be treated as TextRepresentable:

现在Dice类型的实例可被当作是TextRepresentable类型：

    let d12 = Dice(sides: 12, generator:             LinearCongruentialGenerator())
    println(d12.asText())
    // prints "A 12-sided dice"
    
Similarly, the SnakesAndLadders game class can be extended to adopt and conform to the TextRepresentable protocol:

同样，SnakesAndLadders类也可以扩展为适配且遵循TextRepresentable协议：

    extension SnakesAndLadders: TextRepresentable {
        func asText() -> String {
            return "A game of Snakes and Ladders with \(finalSquare) squares"
        }
    }
    println(game.asText())
    // prints "A game of Snakes and Ladders with 25 squares"
    
Declaring Protocol Adoption with an Extension

通过扩展声明协议适配

If a type already conforms to all of the requirements of a protocol, but has not yet stated that it adopts that protocol, you can make it adopt the protocol with an empty extension:

若一个类型已经遵循了一个协议的所有要求，但未声明此类型适配这个协议，你可以使用一个空的扩展来让其适配协议。

    struct Hamster {
        var name: String
        func asText() -> String {
            return "A hamster named \(name)"
        }
    }
    extension Hamster: TextRepresentable {}
    
Instances of Hamster can now be used wherever TextRepresentable is the required type:

从现在起，Hamster的实例可以作为TextRepresentable所需要的类型来使用

    let simonTheHamster = Hamster(name: "Simon")
    let somethingTextRepresentable: TextRepresentable = simonTheHamster
    println(somethingTextRepresentable.asText())
    // prints "A hamster named Simon"
    
NOTE
注意

Types do not automatically adopt a protocol just by satisfying its requirements. They must always explicitly declare their adoption of the protocol.

注意: 即使满足了协议的所有要求，类型也不会自动适配一个协议，因此你必须显式的声明协议适配。

Collections of Protocol Type

集合中的协议类型

A protocol can be used as the type to be stored in a collection such as an array or a dictionary, as mentioned in Protocols as Types. This example creates an array of TextRepresentable things:

协议可以作为集合（数组，字典）内所存储的类型使用，就像之前所讲的一样，协议作为类型使用:

    let things: TextRepresentable[] = [game, d12, simonTheHamster]
    
It is now possible to iterate over the items in the array, and print each item’s textual representation:

如下所示，可以遍历things数组的元素，并打印每个元素的文本（通过asText方法）
    
    for thing in things {
        println(thing.asText())
    }
    // A game of Snakes and Ladders with 25 squares
    // A 12-sided dice
    // A hamster named Simon
    
Note that the thing constant is of type TextRepresentable. It is not of type Dice, or DiceGame, or Hamster, even if the actual instance behind the scenes is of one of those types. Nonetheless, because it is of type TextRepresentable, and anything that is TextRepresentable is known to have an asText method, it is safe to call thing.asText each time through the loop.

注意,thing常量是TextRepresentable类型的。它并非Dice、DiceGame或Hamster类型,即使thing所代表的实例，背后其实是其中一个类型。
尽管如此,因为thing是TextRepresentable协议类型,此类型都包含asText方法,因此在每次循环中可以安全的调用一次asText方法

Protocol Inheritance
协议继承

A protocol can inherit one or more other protocols and can add further requirements on top of the requirements it inherits. The syntax for protocol inheritance is similar to the syntax for class inheritance, but with the option to list multiple inherited protocols, separated by commas:

协议能够继承一或多个其他协议,也可进一步在继承的协议上添加更多的需求。语法与类的继承相似，此外可以用逗号`，`分隔表示继承多个协议

    protocol InheritingProtocol: SomeProtocol, AnotherProtocol {
        // protocol definition goes here
    }
    
Here’s an example of a protocol that inherits the TextRepresentable protocol from above:
下面的例子中，一个协议继承了之前的TextRepresentable协议：

    protocol PrettyTextRepresentable: TextRepresentable {
        func asPrettyText() -> String
    }
    
This example defines a new protocol, PrettyTextRepresentable, which inherits from TextRepresentable. Anything that adopts PrettyTextRepresentable must satisfy all of the requirements enforced by TextRepresentable, plus the additional requirements enforced by PrettyTextRepresentable. In this example, PrettyTextRepresentable adds a single requirement to provide an instance method called asPrettyText that returns a String.

这个例子定义了一个新的协议PrettyTextRepresentable,继承自TextRepresentable。若适配PrettyTextRepresentable协议，必须同时满足TextRepresentable协议的需求,且满足由PrettyTextRepresentable添加的额外需求。在这个例子中,PrettyTextRepresentable添加了另一需求，要求提供一个称为asPrettyText的实例方法，用于返回一个字符串。
The SnakesAndLadders class can be extended to adopt and conform to PrettyTextRepresentable:
可以扩展SnakesAndLadders类，来使之适配且遵循PrettyTextRepresentable协议。

    extension SnakesAndLadders: PrettyTextRepresentable {
        func asPrettyText() -> String {
            var output = asText() + ":\n"
            for index in 1...finalSquare {
                switch board[index] {
                case let ladder where ladder > 0:
                    output += "▲ "
                case let snake where snake < 0:
                    output += "▼ "
                default:
                    output += "○ "
                }
            }
            return output
        }
    }
    
This extension states that it adopts the PrettyTextRepresentable protocol and provides an implementation of the asPrettyText method for the SnakesAndLadders type. Anything that is PrettyTextRepresentable must also be TextRepresentable, and so the asPrettyText implementation starts by calling the asText method from the TextRepresentable protocol to begin an output string. It appends a colon and a line break, and uses this as the start of its pretty text representation. It then iterates through the array of board squares, and appends an emoji representation for each square:

这个扩展声明其适配PrettyTextRepresentable协议，并提供了SnakesAndLadders类型PrettyText方法的一个实现。任何PrettyTextRepresentable协议也是TextRepresentable的扩展,所以，asPrettyText方法的实现过程是这样的：首先调用来自TextRepresentable协议的asText方法开始输出字符串。方法的输出会附加一个冒号和一个换行符,使用这个作为美化文本输出的开始。然后遍历这个方格板数组中的每一个格子,用一个符号来表示:

If the square’s value is greater than 0, it is the base of a ladder, and is represented by ▲.
If the square’s value is less than 0, it is the head of a snake, and is represented by ▼.
Otherwise, the square’s value is 0, and it is a “free” square, represented by ○.
The method implementation can now be used to print a pretty text description of any SnakesAndLadders instance:

当遍历出的元素的值大于0时，表示一个梯子的底部，用`▲`符号表示
当遍历出的元素的值小于0时，表示一个蛇头，用`▲`符号表示
当遍历出的元素的值等于0时，表示一个空白方块，用`○`符号表示

    println(game.asPrettyText())
    // A game of Snakes and Ladders with 25 squares:
    // ○ ○ ▲ ○ ○ ▲ ○ ○ ▲ ▲ ○ ○ ○ ▼ ○ ○ ○ ○ ▼ ○ ○ ▼ ○ ▼ ○

Protocol Composition
协议合成

It can be useful to require a type to conform to multiple protocols at once. You can combine multiple protocols into a single requirement with a protocol composition. Protocol compositions have the form protocol<SomeProtocol, AnotherProtocol>. You can list as many protocols within the pair of angle brackets (<>) as you need, separated by commas.

有一种很有用的方式，来表示一种适配多个协议的类型。你可以使用协议合成（Protocol Composition）来组合多个协议。
协议合成的格式为protocal`<SomeProtocol,AnotherProtocol>`。你可以在尖括号（`<>`）内列出多个协议，用逗号`,`分隔。



Here’s an example that combines two protocols called Named and Aged into a single protocol composition requirement on a function parameter:

下面的例子中，把两个协议Named与Aged组合为一个协议合成，并作为函数的参数使用

    protocol Named {
        var name: String { get }
    }
    protocol Aged {
        var age: Int { get }
    }
    struct Person: Named, Aged {
        var name: String
        var age: Int
    }
    func wishHappyBirthday(celebrator: protocol<Named, Aged>) {
        println("Happy birthday \(celebrator.name) - you're \(celebrator.age)!")
    }
    let birthdayPerson = Person(name: "Malcolm", age: 21)
    wishHappyBirthday(birthdayPerson)
    // prints "Happy birthday Malcolm - you're 21!"
    
    
This example defines a protocol called Named, with a single requirement for a gettable String property called name. It also defines a protocol called Aged, with a single requirement for a gettable Int property called age. Both of these protocols are adopted by a structure called Person.

这个例子中，定义了一个Named协议，要求一个可读的String类型的属性`name`。同时定义了一个Aged协议，要求一个可读的Int类型的属性`Aged`。两个协议被`Person`结构体所适配。

The example also defines a function called wishHappyBirthday, which takes a single parameter called celebrator. The type of this parameter is protocol<Named, Aged>, which means “any type that conforms to both the Named and Aged protocols.” It doesn’t matter what specific type is passed to the function, as long as it conforms to both of the required protocols.

这个例子也定义了带有参数`celebrator`的函数`wishHappyBirthday`。参数的类型是`protocol<Named, Aged>`,表示任何同时遵循Named与Aged协议的类型。不管向函数传递何种参数，只要遵循两个协议即可。


The example then creates a new Person instance called birthdayPerson and passes this new instance to the wishHappyBirthday function. Because Person conforms to both protocols, this is a valid call, and the wishHappyBirthday function is able to print its birthday greeting.

这个例子也创建了一个`Person`的实例`birthdayPerson`,且将这个实例作为参数传入`wishHappyBirthday`函数。因为Person同时适配
两个协议，因此函数可以正常调用，并打印一个生日祝福。

NOTE
注意

Protocol compositions do not define a new, permanent protocol type. Rather, they define a temporary local protocol that has the combined requirements of all protocols in the composition.

注意: 协议合成并不会生成一个新的协议类型，而是将多个协议合成为一个临时协议。

Checking for Protocol Conformance

协议遵循检查

You can use the is and as operators described in Type Casting to check for protocol conformance, and to cast to a specific protocol. Checking for and casting to a protocol follows exactly the same syntax as checking for and casting to a type:

你可以使用类型检查中介绍的`is`,`as`操作符，来检测某类型是否遵循某协议，

The is operator returns true if an instance conforms to a protocol and returns false if it does not.
The as? version of the downcast operator returns an optional value of the protocol’s type, and this value is nil if the instance does not conform to that protocol.
The as version of the downcast operator forces the downcast to the protocol type and triggers a runtime error if the downcast does not succeed.

is操作符用于检查实例是否遵循某个协议，若不遵循则返回`false`。
as?根据协议类型返回一个可选值，当实例遵循协议时，返回该协议类型;否则返回nil
as操作符可以对协议类型进行强制向下转型。若若换失败则会报一个运行时错误。

> 译者注： 向下转型就是把基类转换到继承类，向上转型就是把继承类转换为基类。

This example defines a protocol called HasArea, with a single property requirement of a gettable Double property called area:

下面的例子定义了协议HasArea，需要一个可读的Double类型的属性area。

    @objc protocol HasArea {
        var area: Double { get }
    }
    
NOTE
注意
You can check for protocol conformance only if your protocol is marked with the @objc attribute, as seen for the HasArea protocol above. This attribute indicates that the protocol should be exposed to Objective-C code and is described in Using Swift with Cocoa and Objective-C. Even if you are not interoperating with Objective-C, you need to mark your protocols with the @objc attribute if you want to be able to check for protocol conformance.

注意: 只有用`@objc`属性标注的协议，才可以做协议遵循检查。这个属性表示协议会暴露给Objective-C的代码，可以参考Using Siwft with Cocoa and Objectivei-c。即使你不打算与 Objective-C进行交互，当你需要进行协议遵循检查时，也要在协议前面添加`@objc`.

Note also that @objc protocols can be adopted only by classes, and not by structures or enumerations. If you mark your protocol as @objc in order to check for conformance, you will be able to apply that protocol only to class types.

还要注意一点，`@objc`协议只适用于类,不能用于结构体或枚举。因此只有协议被应用在类上，才能使用`@objc`检查协议的遵循。

Here are two classes, Circle and Country, both of which conform to the HasArea protocol:

下面两个类`Circle`与`Country`都遵循`HasArea`协议

    class Circle: HasArea {
        let pi = 3.1415927
        var radius: Double
        var area: Double { return pi * radius * radius }
        init(radius: Double) { self.radius = radius }
    }
    class Country: HasArea {
        var area: Double
        init(area: Double) { self.area = area }
    }
    
The Circle class implements the area property requirement as a computed property, based on a stored radius property. The Country class implements the area requirement directly as a stored property. Both classes correctly conform to the HasArea protocol.

`Circle`类把`area`属性实现为基于存储属性 `radius`的计算属性，  `Country`类则把`area`属性直接实现为存储型属性。这两个类都遵循`haxArea`协议。


Here’s a class called Animal, which does not conform to the HasArea protocol:

这个例子中`Animal`类不遵循`HasArea`协议：

    class Animal {
        var legs: Int
        init(legs: Int) { self.legs = legs }
    }
    
The Circle, Country and Animal classes do not have a shared base class. Nonetheless, they are all classes, and so instances of all three types can be used to initialize an array that stores values of type AnyObject:
`Circle`类，`Country`类，`Animal`类并没有一个相同的基类，可以采用`AnyObject`类型的数组来承载他们构造后的实例:

    let objects: AnyObject[] = [
        Circle(radius: 2.0),
        Country(area: 243_610),
        Animal(legs: 4)
    ]
The objects array is initialized with an array literal containing a Circle instance with a radius of 2 units; a Country instance initialized with the surface area of the United Kingdom in square kilometers; and an Animal instance with four legs.

The objects array can now be iterated, and each object in the array can be checked to see if it conforms to the HasArea protocol:

objects数组使用数组字面量(array literal)初始化，数组包含一个`radius`为2的`Circle`  实例，aear属性等于英国面积的`Country`实例和一个`legs`属性为4的`Animal`实例。

现在objects数组可以被迭代，且可以对迭代出的每一个元素进行检查，看其是否遵循了`HasArea`协议:

    for object in objects {
        if let objectWithArea = object as? HasArea {
            println("Area is \(objectWithArea.area)")
        } else {
            println("Something that doesn't have an area")
        }
    }
    // Area is 12.5663708
    // Area is 243610.0
    // Something that doesn't have an area
    
Whenever an object in the array conforms to the HasArea protocol, the optional value returned by the as? operator is unwrapped with optional binding into a constant called objectWithArea. The objectWithArea constant is known to be of type HasArea, and so its area property can be accessed and printed in a type-safe way.

Note that the underlying objects are not changed by the casting process. They continue to be a Circle, a Country and an Animal. However, at the point that they are stored in the objectWithArea constant, they are only known to be of type HasArea, and so only their area property can be accessed.

迭代出的元素使用可选绑定(optional binding)将其绑定到`objectWithArea`常量上，使用as?操作符判断其是否遵循`HasArea`协议。`objectWithArea`常量是遵循HasArea协议类型的实例，因此其`area`属性是可以被访问和打印的。

`objects`数组中元素的类型并不会因为向下转型而改变，它们仍然是`Circle`，`Country`，`Animal`类型。然而，当它们被存储到`objectWithArea`常量后，只会被认为是`HasArea`类型，因此只有`area`属性能够被访问。
Optional Protocol Requirements

可选的协议要求

You can define optional requirements for protocols, These requirements do not have to be implemented by types that conform to the protocol. Optional requirements are prefixed by the @optional keyword as part of the protocol’s definition.

您可以定义可选的协议要求,这些要求不需要类型实现符合协议。可选要求使用`@optional`关键字,作为协议的定义的一部分。

An optional protocol requirement can be called with optional chaining, to account for the possibility that the requirement was not implemented by a type that conforms to the protocol. For information on optional chaining, see Optional Chaining.

You check for an implementation of an optional requirement by writing a question mark after the name of the requirement when it is called, such as someOptionalMethod?(someArgument). Optional property requirements, and optional method requirements that return a value, will always return an optional value of the appropriate type when they are accessed or called, to reflect the fact that the optional requirement may not have been implemented.

可选协议要求通过可选链(optional chaining)进行调用，为一个类型实现不遵循协议预留可能，详细内容可以参考可选链章节。

你可以在实现名称后加上?来检查该实现，比如`someOptionalMethod?(someArgument)`。可选方法需求和可选属性要求，在调用或访问时都会返回一个可选值(optional value)，当可选的要求可能没有被实施时，这个值也会反映出来。



NOTE

Optional protocol requirements can only be specified if your protocol is marked with the @objc attribute. Even if you are not interoperating with Objective-C, you need to mark your protocols with the @objc attribute if you want to specify optional requirements.

注意: 可选协议要求只能在含有`@objc`前缀的协议中指定。即使你不准备与Objective－c进行交互，当你要指定可选协议需求时，也需要添加这个前缀。

Note also that @objc protocols can be adopted only by classes, and not by structures or enumerations. If you mark your protocol as @objc in order to specify optional requirements, you will only be able to apply that protocol to class types.

还要注意，`@objc`协议只适用于类,不能用于结构体或枚举。因此只有协议被应用在类上，才能通过`@objc`指定可选协议要求。

The following example defines an integer-counting class called Counter, which uses an external data source to provide its increment amount. This data source is defined by the CounterDataSource protocol, which has two optional requirements:

下面的例子定义了一个计数器类`Counter`,它使用一个外部数据源提供其增量。这个数据源是`CounterDataSource`定义的协议,它有两个可选的要求:

    @objc protocol CounterDataSource {
        @optional func incrementForCount(count: Int) -> Int
        @optional var fixedIncrement: Int { get }
    }
    
The CounterDataSource protocol defines an optional method requirement called incrementForCount and an optional property requirement called fixedIncrement. These requirements define two different ways for data sources to provide an appropriate increment amount for a Counter instance.

`CounterDataSource`协议定义了一个可选的方法要求incrementForCount和一个可选的属性要求`fixedIncrement` 。这些要求定义了两种不同的方式的数据源，来给Counter实例提供一个适当的增量。


NOTE
注意
Strictly speaking, you can write a custom class that conforms to CounterDataSource without implementing either protocol requirement. They are both optional, after all. Although technically allowed, this wouldn’t make for a very good data source.

严格来讲,你可以实现一个类来适配协议`CounterDataSource`,而不去实现协议中的两个要求，因为`CounterDataSource`中的属性和方法要求都是可选的。尽管这样写是可以的，但这并不是一个好的数据源的实现。

The Counter class, defined below, has an optional dataSource property of type CounterDataSource?:
Counter类含有`CounterDataSource?`类型的可选属性`dataSource`，如下所示:

    @objc class Counter {
        var count = 0
        var dataSource: CounterDataSource?
        func increment() {
            if let amount = dataSource?.incrementForCount?(count) {
                count += amount
            } else if let amount = dataSource?.fixedIncrement? {
                count += amount
            }
        }
    }
The Counter class stores its current value in a variable property called count. The Counter class also defines a method called increment, which increments the count property every time the method is called.

`Counter`类通过`count`属性来存储当前值，`increment`方法在每次调用后增加`count`的值。


The increment method first tries to retrieve an increment amount by looking for an implementation of the incrementForCount method on its data source. The increment method uses optional chaining to try to call incrementForCount, and passes the current count value as the method’s single argument.

`increment`方法首先通过可选链调用`incrementForCount`方法内数据源的实现,从而获取增量，并将当前的`count`值作为参数传入方法



Note two levels of optional chaining at play here. Firstly, it is possible that dataSource may be nil, and so dataSource has a question mark after its name to indicate that incrementForCount should only be called if dataSource is non-nil. Secondly, even if dataSource does exist, there is no guarantee that it implements incrementForCount, because it is an optional requirement. This is why incrementForCount is also written with a question mark after its name.

注意，这里有两级可选链。首先,`dataSource`可能为`nil`,所以`dataSource`后使用问好，表明只有在`dataSource`不为`nil`时才调用`incrementForCount`方法。其次,即使`dataSource`存在,也不能保证它实现了`incrementForCount`方法,因为这是一个可选的要求。这就是为什么`incrementForCount`的名字后面也跟着一个问号。

Because the call to incrementForCount can fail for either of these two reasons, the call returns an optional Int value. This is true even though incrementForCount is defined as returning a non-optional Int value in the definition of CounterDataSource.

以上原因表明，即使`CounterDataSource`协议中`incrementForCount`方法被定义为返回一个非可选的Int类型的值，在调用`incrementForCount`方法后，也会返回一个Int类型的可选值。

After calling incrementForCount, the optional Int that it returns is unwrapped into a constant called amount, using optional binding. If the optional Int does contain a value—that is, if the delegate and method both exist, and the method returned a value—the unwrapped amount is added onto the stored count property, and incrementation is complete.

当调用完incrementForCount方法后，返回的可选值通过可选绑定，赋值给常量`amont`。
如果可选值包含值－代表如果代理和方法都存在,方法返回了值－`amount`会赋给存储属性`count`,这个增量过程就完成了。

If it is not possible to retrieve a value from the incrementForCount method—either because dataSource is nil, or because the data source does not implement incrementForCount—then the increment method tries to retrieve a value from the data source’s fixedIncrement property instead. The fixedIncrement property is also an optional requirement, and so its name is also written using optional chaining with a question mark on the end, to indicate that the attempt to access the property’s value can fail. As before, the returned value is an optional Int value, even though fixedIncrement is defined as a non-optional Int property as part of the CounterDataSource protocol definition.

如果不能从incrementForCount方法获取到值 -可能`dataSource`为`nil`,或dataSource没有实现`incrementForCount方法`-increment方法会尝试从数据源中获取fixedIncrement属性的值来代替。`fixedIncrement`属性也是一个可选的要求,所以它也使用可选链，以一个问号结束,表明试图访问属性的值时可以失败。和之前一样,即使`CounterDataSource`协议中，`fixedIncrement`属性被定义为返回一个非可选的Int类型的值，返回值也是一个可选的Int类型的值。

Here’s a simple CounterDataSource implementation where the data source returns a constant value of 3 every time it is queried. It does this by implementing the optional fixedIncrement property requirement:

这里有一个简单的CounterDataSource的实现，通过实现了可选属性fixedIncrement，每次查询都会返回一个常量3。

    class ThreeSource: CounterDataSource {
        let fixedIncrement = 3
    }

You can use an instance of ThreeSource as the data source for a new Counter instance:

你可以使用ThreeSource的实例作为Counter实例的数据源:
    
        var counter = Counter()
        counter.dataSource = ThreeSource()
        for _ in 1...4 {
            counter.increment()
            println(counter.count)
        }
        // 3
        // 6
        // 9
        // 12
    
The code above creates a new Counter instance; sets its data source to be a new ThreeSource instance; and calls the counter’s increment method four times. As expected, the counter’s count property increases by three each time increment is called.

上面的代码创建了一个新的Counter实例，同时把数据源设置为ThreeSource的实例，之后调用了四次计数器的increment方法。正如我们所期望的，increment方法调用一次，计数器的count属性会增加3。

Here’s a more complex data source called TowardsZeroSource, which makes a Counter instance count up or down towards zero from its current count value:
这里有一个更加复杂的数据源例子`TowardsZeroSource`，使计数器实例会从当前计数值向上或向下计数，直到零:

    class TowardsZeroSource: CounterDataSource {
        func incrementForCount(count: Int) -> Int {
            if count == 0 {
                return 0
            } else if count < 0 {
                return 1
            } else {
                return -1
            }
        }
    }
The TowardsZeroSource class implements the optional incrementForCount method from the CounterDataSource protocol and uses the count argument value to work out which direction to count in. If count is already zero, the method returns 0 to indicate that no further counting should take place.

You can use an instance of TowardsZeroSource with the existing Counter instance to count from -4 to zero. Once the counter reaches zero, no more counting takes place:

`TowardsZeroSource`类实现了`CounterDataSource`协议中可选的`incrementForCount`方法，使用`count`参数值来决定计数方向。如果`count`已经是零,方法返回0,表明不会有进一步计算了。
　　
　你可以在`Counter`实例中使用`TowardsZeroSource`实例，从-4计数至零。一旦计数器达到零就不会在计数了:

    counter.count = -4
    counter.dataSource = TowardsZeroSource()
    for _ in 1...5 {
        counter.increment()
        println(counter.count)
    }
    // -3
    // -2
    // -1
    // 0
    // 0
