* ` Memberwise Initializers for Structure Types` 引自 `Initialization`，中文翻译参考了刘康的`《结构类型的成员式构造方法》`
* `Initializers`: 构造方法
* `raw Character`: 字符？ 原生字符？
* `raw Int`: 整型？原生整型？
* `computed property`: 计算属性？ 

> 备注：   
> 以下翻译并未遵循英文的第二人称叙事方式，整体使用第一人称讲述嵌套类型。   
> 由于中英文表达的差异，为兼顾译文的流畅性，本人擅自改动了一些原文的语言结构。更正时还请麻烦告知我，鄙人渴望多听取专家意见、希望在翻译的道路上越走越深~ 谢谢~


#Nested Types
#嵌套类型

Enumerations are often created to support a specific class or structure’s functionality. Similarly, it can be convenient to define utility classes and structures purely for use within the context of a more complex type. To accomplish this, Swift enables you to define nested types, whereby you nest supporting enumerations, classes, and structures within the definition of the type they support.

我们常常创建枚举类型来支持特定类或结构体的功能。同样的，枚举类型可以被方便的用于定义工具类（utility classes）和结构体，而这些工具类和结构体仅仅用在更复杂类型的上下文中。为实现这些功能，Swift可以定义嵌套类型，因此我们可以把枚举类型、类、结构体嵌套到支持他们的类型的定义中。

To nest a type within another type, write its definition within the outer braces of the type it supports. Types can be nested to as many levels as are required.

要嵌套一个类型到另一个类型，只需把它的定义写在外层类型的大括号{}内，这个操作有个前提：外层类型支持嵌套内层类型。嵌套类型没有层数限制，想嵌多少层都可以。

##Nested Types in Action
##嵌套类型实例

The example below defines a structure called `BlackjackCard`, which models a playing card as used in the game of Blackjack. The `BlackJack` structure contains two nested enumeration types called `Suit` and `Rank`.

下面的例子定义了一个`BlackjackCard`（21点牌）的结构体，来模仿21点出牌。`BlackJack`结构体包含了两个嵌套类型`Suit`和`Rank`。

In Blackjack, the Ace cards have a value of either one or eleven. This feature is represented by a structure called Values, which is nested within the Rank enumeration:

在21点规则中，A牌（Ace）即可算作1点也可算作11点。这一特征用一个嵌套在枚举类型Rank中的结构体Values来代表。

```
struct BlackjackCard {
    
    // nested Suit enumeration
    enum Suit: Character {
        case Spades = "♠", Hearts = "♡", Diamonds = "♢", Clubs = "♣"
    }
    
    // nested Rank enumeration
    enum Rank: Int {
        case Two = 2, Three, Four, Five, Six, Seven, Eight, Nine, Ten
        case Jack, Queen, King, Ace
        struct Values {
            let first: Int, second: Int?
        }
        var values: Values {
        switch self {
        case .Ace:
            return Values(first: 1, second: 11)
        case .Jack, .Queen, .King:
            return Values(first: 10, second: nil)
        default:
            return Values(first: self.toRaw(), second: nil)
            }
        }
    }
    
    // BlackjackCard properties and methods
    let rank: Rank, suit: Suit
    var description: String {
    var output = "suit is \(suit.toRaw()),"
        output += " value is \(rank.values.first)"
        if let second = rank.values.second {
            output += " or \(second)"
        }
        return output
    }
}

```

```
struct BlackjackCard {
    
    // nested Suit enumeration
    enum Suit: Character {
        case Spades = "♠", Hearts = "♡", Diamonds = "♢", Clubs = "♣"
    }
    
    // nested Rank enumeration
    enum Rank: Int {
        case Two = 2, Three, Four, Five, Six, Seven, Eight, Nine, Ten
        case Jack, Queen, King, Ace
        struct Values {
            let first: Int, second: Int?
        }
        var values: Values {
        switch self {
        case .Ace:
            return Values(first: 1, second: 11)
        case .Jack, .Queen, .King:
            return Values(first: 10, second: nil)
        default:
            return Values(first: self.toRaw(), second: nil)
            }
        }
    }
    
    // BlackjackCard的属性和方法
    let rank: Rank, suit: Suit
    var description: String {
    var output = "suit is \(suit.toRaw()),"
        output += " value is \(rank.values.first)"
        if let second = rank.values.second {
            output += " or \(second)"
        }
        return output
    }
}

```

The `Suit` enumeration describes the four common playing card suits, together with a raw `Character` value to represent their symbol.

枚举类型`Suit`描述了扑克牌中的4种花色，每一种花色用一个`字符`（Character）代表。

The `Rank` enumeration describes the thirteen possible playing card ranks, together with a raw `Int` value to represent their face value. (This raw `Int` value is not used for the Jack, Queen, King, and Ace cards.)

枚举类型`Rank`描述了相同花色的13张牌，每张牌的面值用一个`整型值`（Int）代表。（这个整型值不用再J、Q、K、A这四张牌上。）

As mentioned above, the `Rank` enumeration defines a further nested structure of its own, called `Values`. This structure encapsulates the fact that most cards have one value, but the Ace card has two values. The `Values` structure defines two properties to represent this:

* `first`, of type `Int`
* `second`, of type `Int?`, or “optional `Int`”

如上所述，枚举类型`Rank`定义了一个内嵌的结构体`Values`。结构体`Values`通过定义两个属性描述了一个实事：大部分牌只有一个面值，而A牌有两个面值。属性如下：

* `first`, `Int`型
* `second`, `Int?`型，或者 “optional `Int`”


`Rank` also defines a computed property, `values`, which returns an instance of the `Values` structure. This computed property considers the rank of the card and initializes a new `Values` instance with appropriate values based on its rank. It uses special values for `Jack`, `Queen`, `King`, and `Ace`. For the numeric cards, it uses the rank’s raw `Int` value.

`Rank`还定义了一个返回结构体`Values`实例的计算属性`values`。这个计算属性依据扑克牌的点数，初始化一个基于扑克牌点数推算出正确值的`Values`实例。计算属性`values`赋予J、Q、K和A这四张牌特定的值，赋予其他数字牌rank中定义的原始整型值（raw `Int`）。

The `BlackjackCard` structure itself has two properties—`rank` and `suit`. It also defines a computed property called `description`, which uses the values stored in `rank` and `suit` to build a description of the name and value of the card. The `description` property uses optional binding to check whether there is a second value to display, and if so, inserts additional description detail for that second value.

结构体`BlackjackCard`定义了两个属性`rank`和`suit`，同时还定义了一个计算属性`description`，这个计算属性使用了`rank`和`suit`中存储的值来描述扑克牌的花色和点数。`description`使用可选绑定（optional binding）来判断是否存在第二个值，如果存在，则为第二个值插入额外的描述。

Because `BlackjackCard` is a structure with no custom initializers, it has an implicit memberwise initializer, as described in [Memberwise Initializers for Structure Types](). You can use this initializer to initialize a new constant called `theAceOfSpades`:

因为结构体`BlackjackCard`没有自定义构造方法，所以它有一个默认的成员式构造方法（memberwise initializer），正如[《结构类型的成员式构造方法》]()所描述的。我们可以使用这个构造方法创建一个新的常量（constant）`theAceOfSpades`：

```
let theAceOfSpades = BlackjackCard(rank: .Ace, suit: .Spades)
println("theAceOfSpades: \(theAceOfSpades.description)")
// prints "theAceOfSpades: suit is ♠, value is 1 or 11

```

```
let theAceOfSpades = BlackjackCard(rank: .Ace, suit: .Spades)
println("theAceOfSpades: \(theAceOfSpades.description)")
// 输出 "theAceOfSpades: suit is ♠, value is 1 or 11

```

Even though `Rank` and `Suit` are nested within `BlackjackCard`, their type can be inferred from context, and so the initialization of this instance is able to refer to the enumeration members by their member names (`.Ace` and `.Spades`) alone. In the example above, the `description` property correctly reports that the Ace of Spades has a value of `1` or `11`.

即使`Rank`和`Suit`被嵌套在`BlackjackCard`里，他们依然可以被~~更外层的~~上下文引用。所以构造`BlackjackCard`实例时，可以仅通过成员名称（`.Ace` 和 `.Spades`）来引用枚举类型的成员。上面的例子中，属性`description`如我们所愿，输出了黑桃A的值`1`或`11`。

##Referring to Nested Types
##引用嵌套类型

To use a nested type outside of its definition context, prefix its name with the name of the type it is nested within:

外部引用嵌套类型时，仅需在其名称前加上外层类型的名称即可：

```
let heartsSymbol = BlackjackCard.Suit.Hearts.toRaw()
// heartsSymbol is "♡"
```

For the example above, this enables the names of `Suit`, `Rank`, and `Values` to be kept deliberately short, because their names are naturally qualified by the context in which they are defined.

正如上例所示，嵌套类型的引用方式可以使`Suit`、`Rank`和`Values`的名字尽可能的简短，因为他们的名字会自然地被所定义的上下文限制。

