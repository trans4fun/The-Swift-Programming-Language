http://numbbbbb.github.io/the-swift-programming-language-in-chinese/chapter2/21_Protocols.html

https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Protocols.html#//apple_ref/doc/uid/TP40014097-CH25-XID_345

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

FullyNamed协议可以定义任何需要一个完整name的类型(方法，属性或者其他需求)。这个协议并不指定什么，只有一个需求：这个类型本身必须提供一个完整的名称。这个需求通过声明一个String类型的实例属性fullName,且这个属性必须是可读的(gettable)来指定。



Here’s an example of a simple structure that adopts and conforms to the FullyNamed protocol:

下面的例子中，一个简单的结构体适配且遵循FullyNamed协议

    struct Person: FullyNamed {
        var fullName: String
    }
    let john = Person(fullName: "John Appleseed")
    // john.fullName is "John Appleseed"

This example defines a structure called Person, which represents a specific named person. It states that it adopts the FullyNamed protocol as part of the first line of its definition.
这个例子中定义了一个名为Person的结构体，代表一个有名字的人。它在第一行的结构体定义中，声明了其适配FullyNamed协议。

Each instance of Person has a single stored property called fullName, which is of type String. This matches the single requirement of the FullyNamed protocol, and means that Person has correctly conformed to the protocol. (Swift reports an error at compile-time if a protocol requirement is not fulfilled.)

每个Person实例都有一个单独存储的，String类型的属性fullName。拥有这个属性代表满足了FullyNamed协议的要求,这意味着Person遵循协议。(在编译时如果不满足协议要求，swift会报告一个错误)。


Here’s a more complex class, which also adopts and conforms to the FullyNamed protocol:
下面有一个更复杂的类,同样适配且遵循FullyNamed协议

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
这个类提供了fullName属性，这个属性是starship这个类的一个只读的计算属性。
每个starship类的实例存储一个强制性的名称和一个可选的前缀。当存在前缀时，fullName属性会把前缀添加到名称前面,从而创建了一个starship的全名。


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

RandomNumberGenerator,该协议要求任何遵循协议的类型调用一个名为random的实例方法,这个方法无论何时调用，都会返回一个Double类型的值。(这个值在0.0与1.0之间，这一点没有在协议中指出)。


The RandomNumberGenerator protocol does not make any assumptions about how each random number will be generated—it simply requires the generator to provide a standard way to generate a new random number.

Here’s an implementation of a class that adopts and conforms to the RandomNumberGenerator protocol. This class implements a pseudorandom number generator algorithm known as a linear congruential generator:

　RandomNumberGenerator协议不会描述如何建立一个随机数，只需要指定一个随机数生成器，从而提供一种标准的方式来生成一个新随机数。
　　
　下面是一个类的实现,遵循RandomNumberGenerator协议。这个类实现了一种伪随机数发生器算法，称为线性同余（linear congruential）发生器:


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


如果你在一个协议中实现的突变方法是为一个类服务的，不需要为其加上mutating关键字。
mutating关键字只用在结构体与枚举类型中。


The example below defines a protocol called Togglable, which defines a single instance method requirement called toggle. As its name suggests, the toggle method is intended to toggle or invert the state of any conforming type, typically by modifying a property of that type.
下面的例子中定义了一个togglable协议，包含一个名为togger的突变实例方法。正如名称所表达的，适配此协议的某实例中，toggle方法通常会通过改变实例的某个属性，来切换或恢复其类型。

The toggle method is marked with the mutating keyword as part of the Togglable protocol definition, to indicate that the method is expected to mutate the state of a conforming instance when it is called:
toggle方法前面加上了mutating关键字，作为Togglabel协议定义的一部分，则表示一个适配toggleabel协议的实例中，这个方法会在调用时改变实例的类型。

    protocol Togglable {
        mutating func toggle()
    }
    
If you implement the Togglable protocol for a structure or enumeration, that structure or enumeration can conform to the protocol by providing an implementation of the toggle method that is also marked as mutating.

当你提供的枚举或结构体遵循Togglabl协议时，需要提供一个带有`mutating`前缀的toggle方法。


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
例子中定义了一个Dice类，用来表示桌游中的拥有N个面的骰子。Dice的实例包含sides和generator两个属性，前者是整型（integer），用来表示骰子有几个面，后者提供了一个随机数生成器，来表示骰子掷出的值。

The generator property is of type RandomNumberGenerator. Therefore, you can set it to an instance of any type that adopts the RandomNumberGenerator protocol. Nothing else is required of the instance you assign to this property, except that the instance must adopt the RandomNumberGenerator protocol.
generator属性的类型为RandomNumberGenerator，因此任何类型，若适配RandomNumberGenerator协议，其实例都可以赋值给generator，除此以外没有其他要求。

Dice also has an initializer, to set up its initial state. This initializer has a parameter called generator, which is also of type RandomNumberGenerator. You can pass a value of any conforming type in to this parameter when initializing a new Dice instance.
Dice类也包含一个构造方法，用于设置其初始状态。这个方法包含一个同样是RandomNumberGenerator类型的参数generator。在构造一个新的Dice的实例时，可以传入任何遵循RandomNumberGenerator协议的类型作为generator。

Dice provides one instance method, roll, which returns an integer value between 1 and the number of sides on the dice. This method calls the generator’s random method to create a new random number between 0.0 and 1.0, and uses this random number to create a dice roll value within the correct range. Because generator is known to adopt RandomNumberGenerator, it is guaranteed to have a random method to call.
Dice类提供了一个实例方法,roll,此方法会返回一个整型值，介于1和骰子面的数量之间。这个方法调用generator的随机�数方法来创建一在0.0和1.0之间的随机数,并使用这个随机数来确保骰子的滚动值在正确的范围内。因为generator适配RandomNumberGenerator协议,因此它可以保证有一个random方法供调用。

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

DiceGame协议可以被任意含有骰子的游戏所适配，DiceGameDelegate协议可以被任意用来追踪DiceGame过程的类型所适配

Here’s a version of the Snakes and Ladders game originally introduced in Control Flow. This version is adapted to use a Dice instance for its dice-rolls; to adopt the DiceGame protocol; and to notify a DiceGameDelegate about its progress:

这里有一个，Snakes and Ladders游戏的新版本（之前的版本在流程控制这一节中介绍过）。新版本使用Dice类的实例作为掷骰子的需求，并且适配了DiceGame协议。同时通知(notify)DiceGameDelegate协议，用来记录游戏过程:

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

This version of the game is wrapped up as a class called SnakesAndLadders, which adopts the DiceGame protocol. It provides a gettable dice property and a play method in order to conform to the protocol. (The dice property is declared as a constant property because it does not need to change after initialization, and the protocol only requires that it is gettable.)

这个版本的游戏封装为SnakesAndLadders类，该类适配DiceGame协议。这个类还提供了可读的dice属性和play方法，从而遵循了DiceGame协议。(dice属性声明为常量，因为构造之后dice属性就不在改变，且协议只要求dice为只读)



The Snakes and Ladders game board setup takes place within the class’s init() initializer. All game logic is moved into the protocol’s play method, which uses the protocol’s required dice property to provide its dice roll values.

Snakes And Ladders游戏通过构造方法(initializer)init初始化游戏。所有的游戏逻辑移到了play方法中，play方法使用协议要求的dice属性，来提供骰子掷出的值。

Note that the delegate property is defined as an optional DiceGameDelegate, because a delegate isn’t required in order to play the game. Because it is of an optional type, the delegate property is automatically set to an initial value of nil. Thereafter, the game instantiator has the option to set the property to a suitable delegate.
注意，delegate并不是玩游戏所必须的，因此delegate被定义为DiceGameDelegate协议类型的可选属性，delegate使用nil作为初始值。此后,游戏实例可以选择将其设置为一个合适的代理。



DiceGameDelegate provides three methods for tracking the progress of a game. These three methods have been incorporated into the game logic within the play method above, and are called when a new game starts, a new turn begins, or the game ends.

DicegameDelegate协议提供了三个方法来跟踪游戏过程。这三个方法存在于游戏的逻辑中，即上面的play()方法内。分别在游戏开始时，新一轮开始时，游戏结束时被调用。


Because the delegate property is an optional DiceGameDelegate, the play method uses optional chaining each time it calls a method on the delegate. If the delegate property is nil, these delegate calls fail gracefully and without error. If the delegate property is non-nil, the delegate methods are called, and are passed the SnakesAndLadders instance as a parameter.
因为delegate属性是一个遵循DiceGameDelegate的可选属性，因此在play()方法中使用了可选链（optional chaining ）来在代理时调用方法。 若delegate属性为nil， 则delegate所调用的方法正常失败（fail gracefully）且不报错。若delegate不为nil，则方法能够被调用，且作为一个参数传入SnakesAndLadders实例中
This next example shows a class called DiceGameTracker, which adopts the DiceGameDelegate protocol:
下一个例子展示了一个名为DiceGameTracker的类，适配DiceGameDelegate协议。

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

在如上所示的gameDidStart实现中，游戏即将开始时使用了game参数来打印一些介绍性信息。game参数拥有一个DiceGame类型,而不是SnakesAndLadders,所以gameDidStart只能访问和使用DiceGame协议中的方法和属性。然而,该方法仍然能够使用类型追溯（type casting）查询底层实例的类型。在这个例子中,它在幕后检查游戏是否是SnakesAndLadders的一个实例,当确认后打印一个适当的消息。

gameDidStart also accesses the dice property of the passed game parameter. Because game is known to conform to the DiceGame protocol, it is guaranteed to have a dice property, and so the gameDidStart method is able to access and print the dice’s sides property, regardless of what kind of game is being played.

gameDidStart也能够访问dice属性，这个属性在被传递为参数的game中。因为game遵循DiceGame协议，因此被赋予了dice属性，不管运行何种游戏，gameDidStart方法都可以访问且打印骰子的边数。
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
