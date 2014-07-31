# 扩展（Extensions）

扩展为已有的类，结构，枚举添加新的功能。其中包括扩展没有代码访问权限的类型（即追溯建模，retroactive modeling）。扩展和 Objective-C 当中的分类（category）很相似。（与 Objective-C 中的分类不同的是，Swift 的扩展没有名字）

Swift 中的扩展可以：
- 增加计算属性和静态计算属性
- 定义实例方法和类型方法
- 提供新的构造器
- 定义下标
- 定义和使用新的嵌套类型
- 将已有的类型转换为符合某一个协议

> <b>提示</b>
> 
> 如果定义一个扩展用来在已有的类型上增加新的功能，那么新功能会应用在所有已经存在的实例上，即使是在扩展被定义之前实例化的。
## 扩展的语法

使用 ``extension`` 关键字来声明扩展：

```
extension SomeType {
    // new functionality to add to SomeType goes here
}
```

一个扩展可以扩展一个已有的类型，使它能适配一个或多个的协议（protocol）。如果是这种情况的话，协议的命名方式应该与类和结构体的命名方式完全一致。

```
extension SomeType: SomeProtocol, AnotherProtocol {
    // implementation of protocol requirements goes here
}
```

这种增加协议一致性（protocol conformance）的方式在 [通过扩展增加协议一致性](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Protocols.html#//apple_ref/doc/uid/TP40014097-CH25-XID_355) 一文中有记述。

## 计算属性（Computed Properties）

扩展可以为已有的类型增加实例计算属性和类型计算属性。这个例子向 Swift 内建类型 ``Double`` 添加五个实例计算类型，用来提供转换为距离单位的基本功能：

```
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
```

这些计算属性表达的是一个 ``Double`` 类型的值是某种长度单位下的值。尽管是计算属性，但他们仍然可以接在一个带有 dot 语法的字面值的后面，用来将字面值转换成距离。

在上述的例子中，``Double`` 类型的 ``1.0`` 代表 “一米” 。这是为什么计算属性 ``m`` 仅仅返回 ``self`` ——表达式 ``1.m`` 最终结果是  ``Double`` 类型的值 ``1.0`` 。

其他单位转换为以米为单位的数值需要进行一些转换。1千米等于1,000米，所以计算属性 ``km`` 要把数值转换成以米为单位，需要把值乘以 ''1_000.00''。同样，1英尺等于 ''3.28084'' 米，所以计算属性 ''ft'' 需要把值除以 ''3.28024'' 才能把英尺转换成米。

因为这些都是只读的计算属性，所以为了简便起见，不需要关键字 ''keyword'' 进行表示。他们的返回值都是 ``Double`` 类型的，所以可以用在所有可以接受 ``Double`` 类型的数学计算中：

```
let aMarathon = 42.km + 195.m
println("A marathon is \(aMarathon) meters long")
// prints "A marathon is 42195.0 meters long"
```

> <b>提示</b>
> 
> 扩展可以添加新的计算属性，但是不能添加存储属性，也不能向已有属性添加属性观察器（property observer）。

## 构造器（Initializers）

扩展能向已有类型添加新的构造器。这允许你用自己定义的类型作为构造器参数扩展其他的类型，或者提供原始实现没有提供的额外的初始化选项

扩展能向类添加新的简便构造器，但是不能添加新的指定构造器或者析构器。指定构造器和析构器必须在类的原始实现中提供。

> <b>提示</b>
> 
> 如果使用扩展向一个值类型添加构造器，该构造器向所有存储属性提供默认值并且未定义任何其他的自定义构造器，你可以调用默认的构造和成员构造器来为你扩展的构造器当中的值类型赋值。
> 正如 [构造器对值类型的构造委托](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Initialization.html#//apple_ref/doc/uid/TP40014097-CH18-XID_281)  一文所说的那样，如果你已经把构造器写成值类型原始实现的一部分，则不符合上述规则。

在下面的例子里，定义了一个用于描述几何矩形的结构体 ``Rect`` 。同时定义了两个辅助性结构体 ``Size``,``Point``，两个结构体当中的属性默认值都为 ``0.0``：

```
struct Size {
    var width = 0.0, height = 0.0
}
struct Point {
    var x = 0.0, y = 0.0
}
struct Rect {
    var origin = Point()
    var size = Size()
}
```

因为 结构体 ``Rect`` 为所有的属性都提供了默认值，正如默认构造器一节所说的，它可以自动接受默认构造器和成员构造器。这些构造器可以用来创建新的 ``Rect`` 实例：

```
let defaultRect = Rect()
let memberwiseRect = Rect(origin: Point(x: 2.0, y: 2.0),
    size: Size(width: 5.0, height: 5.0))
```

你可以使用扩展来为结构体 ``Rect`` 额外提供一个以中心点和大小作为参数的构造器：

```
extension Rect {
    init(center: Point, size: Size) {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}
```

新构造器通过中心点和大小两个参数计算出合适的原点值，然后调用结构体的自动成员构造器 ``init(origin:size:)`` ，把计算出的值存储到合适的属性上：

```
let centerRect = Rect(center: Point(x: 4.0, y: 4.0),
    size: Size(width: 3.0, height: 3.0))
// centerRect's origin is (2.5, 2.5) and its size is (3.0, 3.0)
```


> <b>提示</b>
> 
> 如果使用扩展来提供新的构造器，那么你仍要确保构造过程中，每一个实例都被完全初始化了。


## 方法（Methods）

扩展可以向已有类型添加新的实例方法和类型方法。下面的例子中，向 类型 ``Int`` 中添加了新的实例方法 ``repetitions``：

```
extension Int {
    func repetitions(task: () -> ()) {
        for i in 0..self {
            task()
        }
    }
}
```

``repetitions`` 方法的参数是 ``() -> ()``，说明参数是一个无参数无返回值的函数

扩展被定义之后，你就可以在任何整数上调用 ``repetitions`` 方法，来多次执行某个任务：

```
3.repetitions({
    println("Hello!")
})
// Hello!
// Hello!
// Hello!
```

使用尾随闭包（trailing closure）语法可以使调用更简洁：

```
3.repetitions {
    println("Goodbye!")
}
// Goodbye!
// Goodbye!
// Goodbye!
```

## 可变实例方法（Mutating Instance Methods）

通过扩展添加的实例方法也可以修改实例本身。结构体和枚举类型的方法中改变 ``self`` 或者其中的属性，必须标记实例的方法为 ``mutating`` ，就像原始实现中的声明变异方法（mutating method）一样。

下面的例子为 Swift 中的 ``Int`` 类型添加了一个新的变异方法 ``square``，用来计算原始值的平方：

```
extension Int {
    mutating func square() {
        self = self * self
    }
}
var someInt = 3
someInt.square()
// someInt is now 9
```

## 下标（Subscripts）

扩展可以为已有类型添加新的下标。下面的例子为 Swift 中的内建类型 ``Int`` 添加一个整型下标。下标 ``[n]`` 返回 十进制数从右往左第 n 位上的数字：

- 123456789[0] returns 9
- 123456789[1] returns 8

……以此类推：

```
extension Int {
    subscript(digitIndex: Int) -> Int {
        var decimalBase = 1
            for _ in 1...digitIndex {
                decimalBase *= 10
            }
        return (self / decimalBase) % 10
    }
}
746381295[0]
// returns 5
746381295[1]
// returns 9
746381295[2]
// returns 2
746381295[8]
// returns 7
```

如果该 ``Int`` 值没有足够的位数与请求对应，即下标越界，则下标会返回 ``0`` ，就好像它自动在数字左边补0一样：

```
746381295[9]
// returns 0, as if you had requested:
0746381295[9]
```


## 嵌套类型（Nested Types）

扩展可以向已有的类，结构体和枚举类型添加新的嵌套类型：

```
extension Character {
    enum Kind {
        case Vowel, Consonant, Other
    }
    var kind: Kind {
    switch String(self).lowercaseString {
    case "a", "e", "i", "o", "u":
        return .Vowel
    case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
    "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
        return .Consonant
    default:
        return .Other
        }
    }
}
```

上面的例子为 ``Character`` 添加了新的嵌套枚举。枚举类型的 ``Kind`` 表示一个字符所属的种类。具体来说就是一个字符是拉丁字母的元音，辅音，还是其他种类的字符（不考虑口语和地方变种的情况下）。

这个例子中同时也为 ``Character`` 添加了一个新的实例计算属性 ``kind``，用来返回字符对应的枚举成员 ``Kind``

现在嵌套枚举可以在 ``Character`` 上面使用了：

```
func printLetterKinds(word: String) {
    println("'\(word)' is made up of the following kinds of letters:")
    for character in word {
        switch character.kind {
        case .Vowel:
            print("vowel ")
        case .Consonant:
            print("consonant ")
        case .Other:
            print("other ")
        }
    }
    print("\n")
}
printLetterKinds("Hello")
// 'Hello' is made up of the following kinds of letters:
// consonant vowel consonant consonant vowel
```

``printLetterKinds`` 函数迭代 ``String`` 类型的参数的每一个字母。每次迭代都根据当前字母包含的计算属性 ``kind`` 输出对应的类型描述。这样，``printLetterKinds`` 函数就输出了一个单词内所有字母的类型，正如上面例子中的单词 "word" 一样。


> <b>提示</b>
> 
> 因为已知 ``character.kind`` 的类型是 ``Character.Kind``，所以所有 ``Character.Kind`` 的成员值都可以在 ``switch`` 语句中使用简写形式，比如使用 ``.Vowel`` 来代替 ``Character.Kind.Vowel``。


