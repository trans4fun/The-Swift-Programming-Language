#Generics
#泛型

Generic code enables you to write flexible, reusable functions and types that can work with any type, subject to requirements that you define. You can write code that avoids duplication and expresses its intent in a clear, abstracted manner.

泛型代码可以让你写出更灵活、复用性更强的的函数或者类型，这种函数或者类型可以是满足你需求的任意类型或者主题。你可以用一种清晰抽象的方式表达出来，避免重复代码。

Generics are one of the most powerful features of Swift, and much of the Swift standard library is built with generic code. In fact, you’ve been using generics throughout this Language Guide, even if you didn’t realize it. For example, Swift’s Array and Dictionary types are both generic collections. You can create an array that holds Int values, or an array that holds String values, or indeed an array for any other type that can be created in Swift. Similarly, you can create a dictionary to store values of any specified type, and there are no limitations on what that type can be.

泛型是Swift中非常强大的特性之一，而且很多Swift中的基础库是用泛型构建的。事实上，不管你有没有意识到，其实在整本swift介绍中你都会用到泛型。例如，Swift中的Array和Dictionary类型都是泛型集合。你可以创建一个int类型的数组，也可以创建String类型的数组，事实上在Swift中你可以创建任意类型的数组。同样地，你也可以创建一个存储任意类型数据的字典类型；

#The Problem That Generics Solve
#泛型解决的问题

Here’s a standard, non-generic function called `swapTwoInts`, which swaps two Int values:

下边代码是一个标准的、非泛型函数`swapTwoInts`, 用于交换两个int值：

```
func swapTwoInts(inout a: Int, inout b: Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

This function makes use of in-out parameters to swap the values of a and b, as described in [In-Out Parameters]().

这个函数使用in-out参数交换a,b值，具体的可以参考[In-Out Parameters]().

The `swapTwoInts` function swaps the original value of b into a, and the original value of a into b. You can call this function to swap the values in two Int variables:

`swapTwoInts`函数把b的原始值赋值给a, a的原始值给b.你可以调用这个函数去交换两个整形值：

```
var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
println("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// prints "someInt is now 107, and anotherInt is now 3
```

The `swapTwoInts` function is useful, but it can only be used with Int values. If you want to swap two String values, or two Double values, you have to write more functions, such as the `swapTwoStrings` and `swapTwoDoubles `functions shown below:

`swapTwoInts`函数是有用的，但是这个函数只能交换int值。如果想交换两个NSString、或者是两个Double类型的值，你不得不写更多的代码，比如`swapTwoStrings`,`swapTwoDoublesfunctions`,如下所示：

```
func swapTwoStrings(inout a: String, inout b: String) {
    let temporaryA = a
    a = b
    b = temporaryA
}
func swapTwoDoubles(inout a: Double, inout b: Double) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

You may have noticed that the bodies of the `swapTwoInts`, `swapTwoStrings`, and `swapTwoDoubles` functions are identical. The only difference is the type of the values that they accept (Int, String, and Double).

也许，你已经注意到了，这三个函数的内容基本上是相同的，唯一的区别就是传参类型不一样，分别是Int,String,Double.

It would be much more useful, and considerably more flexible, to write a single function that could swap two values of any type. This is the kind of problem that generic code can solve. (A generic version of these functions is defined below.)

你会想，如果可以只写一个函数就可以交换两个任意类型的值，那一定会很强大、相当的灵活。这正是泛型所解决的问题。(泛型版的这种函数如下）。

```
NOTE
In all three functions, it is important that the types of a and b are defined to be the same as each other. If a and b were not of the same type, it would not be possible to swap their values. Swift is a type-safe language, and does not allow (for example) a variable of type String and a variable of type Double to swap values with each other. Attempting to do so would be reported as a compile-time error.
```


#Generic Functions
#泛型函数

Generic functions can work with any type. Here’s a generic version of the `swapTwoInts` function from above, called `swapTwoValues`:

泛型函数可以工作于任何类型。下面就是上边提到的`swapTwoInts`的泛型版本，`swapTwoValues`：

```
func swapTwoValues<T>(inout a: T, inout b: T) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```
The body of the `swapTwoValues` function is identical to the body of the `swapTwoInts` function. However, the first line of `swapTwoValues` is slightly different from `swapTwoInts`. Here’s how the first lines compare:

除了第一行有一点区别之外，`swapTwoValues`和`swapTwoInts`的主题内容是一样的，如下所示：

```
func swapTwoInts(inout a: Int, inout b: Int)
func swapTwoValues<T>(inout a: T, inout b: T)
```

The generic version of the function uses a placeholder type name (called T, in this case) instead of an actual type name (such as Int, String, or Double). The placeholder type name doesn’t say anything about what T must be, but it does say that both a and b must be of the same type T, whatever T represents. The actual type to use in place of T will be determined each time the `swapTwoValues` function is called.

泛型版本使用了节点类型命名（一般都使用字母T）来代替实际的类型名称（比如Int,String,或者Double）。节点类型定义限制a和b必须是相同类型，而不限制到底是什么类型，T可以代表任意类型。只有当`swapTwoValues`真正调用的时候，才会决定T代表什么类型。

The other difference is that the generic function’s name (swapTwoValues) is followed by the placeholder type name (T) inside angle brackets (<T>). The brackets tell Swift that T is a placeholder type name within the`swapTwoValues` function definition. Because T is a placeholder, Swift does not look for an actual type called T.

另一个区别是泛型函数后边跟着的类型（T）是放到尖括号里边的（<T>）。尖括号告诉Swift，T是`swapTwoValues`所定义的一个节点类型。由于T表示节点，swift不会查找命名为T的类型。

The `swapTwoValues` function can now be called in the same way as `swapTwoInts`, except that it can be passed two values of any type, as long as both of those values are of the same type as each other. Each time `swapTwoValues` is called, the type to use for T is inferred from the types of values passed to the function.



In the two examples below, T is inferred to be Int and String respectively:

```
var someInt = 3
var anotherInt = 107
swapTwoValues(&someInt, &anotherInt)
// someInt is now 107, and anotherInt is now 

var someString = "hello"
var anotherString = "world"
swapTwoValues(&someString, &anotherString)
// someString is now "world", and anotherString is now "hello"
```

```
NOTE
The swapTwoValues function defined above is inspired by a generic function called swap, which is part of the Swift standard library, and is automatically made available for you to use in your apps. If you need the behavior of the swapTwoValues function in your own code, you can use Swift’s existing swap function rather than providing your own implementation.
```
#Type Parameters
#参数类型
In the swapTwoValues example above, the placeholder type T is an example of a type parameter. Type parameters specify and name a placeholder type, and are written immediately after the function’s name, between a pair of matching angle brackets (such as <T>).

Once specified, a type parameter can be used to define the type of a function’s parameters (such as the a and b parameters of the swapTwoValues function); or as the function’s return type; or as a type annotation within the body of the function. In each case, the placeholder type represented by the type parameter is replaced with an actual type whenever the function is called. (In the swapTwoValues example above, T was replaced with Int the first time the function was called, and was replaced with String the second time it was called.)

You can provide more than one type parameter by writing multiple type parameter names within the angle brackets, separated by commas.

‌
#Naming Type Parameters
#参数类型命名
In simple cases where a generic function or generic type needs to refer to a single placeholder type (such as the swapTwoValues generic function above, or a generic collection that stores a single type, such as Array), it is traditional to use the single-character name T for the type parameter. However, you are can use any valid identifier as the type parameter name.

If you are defining more complex generic functions, or generic types with multiple parameters, it can be useful to provide more descriptive type parameter names. For example, Swift’s Dictionary type has two type parameters—one for its keys and one for its values. If you were writing Dictionary yourself, you might name these two type parameters KeyType and ValueType to remind you of their purpose as you use them within your generic code.

```
NOTE

Always give type parameters UpperCamelCase names (such as T and KeyType) to indicate that they are a placeholder for a type, not a value.
```
#Generic Types
#泛型类型
n addition to generic functions, Swift enables you to define your own generic types. These are custom classes, structures, and enumerations that can work with any type, in a similar way to Array and Dictionary.

This section shows you how to write a generic collection type called Stack. A stack is an ordered set of values, similar to an array, but with a more restricted set of operations than Swift’s Array type. An array allows new items to be inserted and removed at any location in the array. A stack, however, allows new items to be appended only to the end of the collection (known as pushing a new value on to the stack). Similarly, a stack allows items to be removed only from the end of the collection (known as popping a value off the stack).

```
NOTE
The concept of a stack is used by the UINavigationController class to model the view controllers in its navigation hierarchy. You call the UINavigationController class pushViewController:animated: method to add (or push) a view controller on to the navigation stack, and its popViewControllerAnimated: method to remove (or pop) a view controller from the navigation stack. A stack is a useful collection model whenever you need a strict “last in, first out” approach to managing a collection.
```

The illustration below shows the push / pop behavior for a stack:

下边图表展示的是堆栈的进入、进出特性：

![stack](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Art/stackPushPop_2x.png)


1. There are currently three values on the stack.
2. A fourth value is “pushed” on to the top of the stack.
3. The stack now holds four values, with the most recent one at the top.
4. The top item in the stack is removed, or “popped”.
5. After popping a value, the stack once again holds three values.

1.当前堆栈里有3个值
2.第四个值从堆栈的顶部push进去
3.现在堆栈中有4个值，其中最先进的在最顶部
4.堆栈最顶部的值被移除，或者叫“popped”
5.当推出一个值后，堆栈重新变成了三个值

Here’s how to write a non-generic version of a “stack, in this case for a stack of Int values

下边是如何写一个不是泛型版本的堆栈，这个例子中得堆栈是Int类型：

```
struct IntStack {
    var items = Int[]()
    mutating func push(item: Int) {
        items.append(item)
    }
    mutating func pop() -> Int {
        return items.removeLast()
    }
}
```
This structure uses an Array property called items to store the values in the stack. Stack provides two methods, push and pop, to push and pop values on and off the stack. These methods are marked as mutating, because they need to modify (or mutate) the structure’s items array.

这个结构中使用数组属性`items`去存储堆栈中的数据。堆栈提供两个方法`push` 和`pop`，用于推入数据到堆栈，或者从堆栈推出数据。这些方法定义为`mutating`类型，原因是需要修改结构中得items数组的值。

The IntStack type shown above can only be 
“used with Int values, however. It would be much more useful to define a generic Stack class, that can manage a stack of any type of value.

上边的这个`IntStack`类型只能用于Int值。然而，定义泛型类型的堆栈类型，可以管理堆栈中得任意类型，是非常有用的。

Here’s a generic version of the same code:

上边是相同代码的泛型版本：

```
struct Stack<T> {
    var items = T[]()
    mutating func push(item: T) {
        items.append(item)
    }
    mutating func pop() -> T {
        return items.removeLast()
    }
}
```
Note how the generic version of Stack is essentially the same as the non-generic version, but with a placeholder type parameter called T instead of an actual type of Int. This “type parameter is written within a pair of angle brackets (<T>) immediately after the structure’s name.

可以注意到，除了使用T代替真实int类型之外，下边的泛型版本的堆栈结构和上边非泛型版本的基本上一样的。这种类型参数是在紧接着结构的名称后跟着一对尖括号（<T>）.

T defines a placeholder name for “some type T” to be provided later on. This future type can be referred to as “T” anywhere within the structure’s definition. In this case, T is used as a placeholder in three places:

`T`定义了一个名称为”某种类型T“的节点提供给后边用。这种将来类型可以在结构体定义中的任何地方表示为`T`。在这个例子中，`T`在如下的几个地方会被使用：

1. To create a property called items, which is initialized with an empty array of values of type T
2. To specify that the push method has a single parameter called item, which must be of type T
3. To specify that the value returned by the pop method will be a value of type T

1.创建成员变量`items`，被初始化为包含类型T的空数组
2.指定`push`方法有一个参数item，类型为T类型
3.指定`pop`方法返回结果类型为T

You create instances of Stack in a similar way to Array and Dictionary, by writing the actual type to be used for this specific stack within angle brackets after the type name when creating a new instance with initializer syntax:

像创建Array和Dictionary一样，创建一个Stack实例，在初始化时，紧随类型名后边尖括号中写出实际用到的类型：

```
var stackOfStrings = Stack<String>()
stackOfStrings.push("uno")
stackOfStrings.push("dos")
stackOfStrings.push("tres")
stackOfStrings.push("cuatro")
// the stack now contains 4 strings
```

Here’s how stackOfStrings looks after pushing these four values on to the stack:

下边展示`stackOfStrings`是如何把四个值push进栈：

![进栈](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Art/stackPushedFourStrings_2x.png)

 Popping a value from the stack returns and removes the top value, "cuatro":
 
 下图是如何从栈中pop一个值的过程，移除栈最顶上结果，“cuatro”,并返回其值：

```
    let fromTheTop = stackOfStrings.pop()
    // fromTheTop is equal to "cuatro", and the stack now contains 3 strings
```
Here’s how the stack looks after popping its top value: 

下边是推出最顶层数据之后的堆栈效果：

![移除堆栈效果](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Art/stackPoppedOneString_2x.png)

 Because it is a generic type, Stack can be used to create a stack of any valid type in Swift, in a similar manner to Array and Dictionary. 
 
 由于`Stack`是泛型类型，所以在Swift中可以用于创建任何有效类型的栈，方式同`Array`和`Dictionary`。

#Type Constraints
#类型约束

The swapTwoValues function and the Stack type can work with any type. However, it is sometimes useful to enforce certain type constraints on the types that can be used with generic functions and generic types. Type constraints specify that a type parameter must inherit from a specific class, or conform to a particular protocol or protocol composition.

`swapTwoValues`函数和`Stack`类型可以作用于任何类型，不过，有的时候对泛型函数和泛型类型上做类型强制约束是非常有用的。类型约束指定参数类型必须继承一个指定类型参数或者遵循一个特定的协议或协议构成。

For example, Swift’s Dictionary type places a limitation on the types that can be used as keys for a dictionary. As described in Dictionaries, the type of a dictionary’s keys must be hashable. That is, it must provide a way to make itself uniquely representable. Dictionary needs its keys to be hashable so that it can check whether it already contains a value for a particular key. Without this requirement, Dictionary could not tell whether it should insert or replace a value for a particular key, nor would it be able to find a value for a given key that is already in the dictionary.

例如，Swift中的`Dictionary`对键值做了约束。在字典的描述中，字典的键值类型必须是可哈希的，就是说他必须有一种方法保证其是唯一的。`Dictionary`约定键值是可哈希的，是为了便于检查其是否已经包含某个特定键的值。如果没有这个约束，就不能告诉是否可以插入或者替换某个特定键的值，也不能查找到某个已经存储在字典中的特定值。

This requirement is enforced by a type constraint on the key type for Dictionary, which specifies that the key type must conform to the Hashable protocol, a special protocol defined in the Swift standard library. All of Swift’s basic types (such as String, Int, Double, and Bool) are hashable by default.

这个需求强制加上一个类型约束作用于Dictionary的键上，而且其键类型必须遵循Hashable协议（Swift 标准库中定义的一个特定协议）。所有的 Swift 基本类型（如String，Int，Double和 Bool）默认都是可哈希。

You can define your own type constraints when creating custom generic types, and these constraints provide much of the power of generic programming. Abstract concepts like Hashable characterize types in terms of their conceptual characteristics, rather than their explicit type.

当你创建自定义泛型类型时，你可以定义你自己的类型约束，当然，这些约束要支持泛型编程的强力特征中的多数。抽象概念如可哈希具有的类型特征是根据它们概念特征来界定的，而不是它们的直接类型特征。

##Type Constraint Syntax

##类型约束语法
 You write type constraints by placing a single class or protocol constraint after a type parameter’s name, separated by a colon, as part of the type parameter list. The basic syntax for type constraints on a generic function is shown below (although the syntax is the same for generic types):
 
 你可以通过在参数名称的后边以冒号分割，加上类型参数约束。基础的泛型函数的类型约束语法如下（同样的，泛型类型的语法相同）

```
    func someFunction<T: SomeClass, U: SomeProtocol>(someT: T, someU: U) {
    // function body goes here
    }
 ```
The hypothetical function above has two type parameters. The first type parameter, T, has a type constraint that requires T to be a subclass of SomeClass. The second type parameter, U, has a type constraint that requires U to conform to the protocol SomeProtocol.

上边函数有两个参数。参数一类型参数为T，需要T必须是`SomeClass`子类；第二个参数类型为U，需要U必须遵循`SomeClass`协议。

##Type Constraints in Action
##类型约束行为

Here’s a non-generic function called findStringIndex, which is given a String value to find and an array of String values within which to find it. The findStringIndex function returns an optional Int value, which will be the index of the first matching string in the array if it is found, or nil if the string cannot be found:

这里有个名为findStringIndex的非泛型函数，该函数是去查找包含一指定String值的数组。若查找到匹配的字符串，findStringIndex函数返回该字符串在数组中的索引位置（Int），反之返回nil：

    func findStringIndex(array: String[], valueToFind: String) -> Int? {
    for (index, value) in enumerate(array) {
    if value == valueToFind {
    return index
    }
    }
    return nil
    }

The findStringIndex function can be used to find a string value in an array of strings:

`findStringIndex`用于查找数组中的指定String值：

    let strings = ["cat", "dog", "llama", "parakeet", "terrapin"]
    if let foundIndex = findStringIndex(strings, "llama") {
    println("The index of llama is \(foundIndex)")
    }
    // prints "The index of llama is 2"

The principle of finding the index of a value in an array isn’t useful only for strings, however. You can write the same functionality as a generic function called findIndex, by replacing any mention of strings with values of some type T instead.

如果只是查找数组中的指定字符串用处不大，但是你可以写出相同功能的泛型版本`findIndex`，用T代替字符串类型。

Here’s how you might expect a generic version of findStringIndex, called findIndex, to be written. Note that the return type of this function is still Int?, because the function returns an optional index number, not an optional value from the array. Be warned, though—this function does not compile, for reasons explained after the example:

下边是你理想中的`findStringIndex`的泛型版本`findIndex`。注意到函数的返回结果仍然是Int?,这是因为这个函数使用用于返回具体的索引值，而不是搜索值。需要提醒的是，这个函数不会编译，原因后边会说明：

    func findIndex<T>(array: T[], valueToFind: T) -> Int? {
    for (index, value) in enumerate(array) {
    if value == valueToFind {
    return index
    }
    }
    return nil
    }

This function does not compile as written above. The problem lies with the equality check, “if value == valueToFind”. Not every type in Swift can be compared with the equal to operator (==). If you create your own class or structure to represent a complex data model, for example, then the meaning of “equal to” for that class or structure is not something that Swift can guess for you. Because of this, it is not possible to guarantee that this code will work for every possible type T, and an appropriate error is reported when you try to compile the code.

这个函数按照上边的写法不会编译。原因是因为比较这部分`“if value == valueToFind”. 不是所有的泛型类型都可以用比较操作`==`。如果你创建了自己的函数或者结构代表一个负责的数据模型，那么Swift语言没法猜出这个类或者结果等于的意思。正因为如此，不能保证这个代码可以作用于所有类型T，而且会编译出错。

All is not lost, however. The Swift standard library defines a protocol called Equatable, which requires any conforming type to implement the equal to operator (==) and the not equal to operator (!=) to compare any two values of that type. All of Swift’s standard types automatically support the Equatable protocol.

不过，有解决方法。Swift 标准库中定义了一个Equatable协议，该协议要求任何遵循的类型实现等式符（==）和不等符（!=）对任何两个该类型进行比较。所有的 Swift 标准类型自动支持Equatable协议。

Any type that is Equatable can be used safely with the findIndex function, because it is guaranteed to support the equal to operator. To express this fact, you write a type constraint of Equatable as part of the type parameter’s definition when you define the function:

任何Equatable类型都可以安全的使用在findIndex函数中，它保证可以支持等号操作。为了说明这个事实，你定义函数时，可以写一个Equatable类型约束作为类型参数定义的一部分：

    func findIndex<T: Equatable>(array: T[], valueToFind: T) -> Int? {
    for (index, value) in enumerate(array) {
    if value == valueToFind {
    return index
    }
    }
    return nil
    }

The single type parameter for findIndex is written as T: Equatable, which means “any type T that conforms to the Equatable protocol.

`findIndex`的类型参数可以写成`T: Equatable`,表示任意实现` Equatable`协议的类型。

The findIndex function now compiles successfully and can be used with any type that is Equatable, such as Double or String:

`findIndex`类型现在可以成功编译，并且可以用于任意实现了` Equatable`协议的类型，比如`Doubl`e 或者`String`:

    let doubleIndex = findIndex([3.14159, 0.1, 0.25], 9.3)
    // doubleIndex is an optional Int with no value, because 9.3 is not in the array
    let stringIndex = findIndex(["Mike", "Malcolm", "Andrea"], "Andrea")
    // stringIndex is an optional Int containing a value of 2

#Associated Types
#关联类型
When defining a protocol, it is sometimes useful to declare one or more associated types as part of the protocol’s definition. An associated type gives a placeholder name (or alias) to a type that is used as part of the protocol. The actual type to use for that associated type is not specified until the protocol is adopted. Associated types are specified with the typealias keyword.

当定义一个协议时，有时声明一个或多个关联类型作为协议的一部分非常有用。一个关联类型给定作用于协议部分的类型一个节点名（或别名）。作用于关联类型实际类型不需要指定，直到协议接受。关联类型被指定为typealias关键字。

##Associated Types in Action
##关联类型行为

Here’s an example of a protocol called Container, which declares an associated type called ItemType:

下边是一个协议`Container`,定义了关联类型`ItemType`:

    protocol Container {
    typealias ItemType
    mutating func append(item: ItemType)
    var count: Int { get }
    subscript(i: Int) -> ItemType { get }
    }

The Container protocol defines three required capabilities that any container must provide:

上述协议定义了三个必须支持的兼容协议：

1. It must be possible to add a new item to the container with an append method.

2. It must be possible to access a count of the items in the container through a count property that returns an Int value.

3. It must be possible to retrieve each item in the container with a subscript that takes an Int index value.

1. 必须可以通过append方法添加新的元素到容器中。
2. 必须提供一个属性方法可以获取容器中的元素数目，并返回一个Int值。
3. 必须可以通过Int索引下标检索每个值。

This protocol doesn’t specify how the items in the container should be stored or what type they are allowed to be. The protocol only specifies the three bits of functionality that any type must provide in order to be considered a Container. A conforming type can provide additional functionality, as long as it satisfies these three requirements.



Any type that conforms to the Container protocol must be able to specify the type of values it stores. Specifically, it must ensure that only items of the right type are added to the container, and it must be clear about the type of the items returned by its subscript.

To define these requirements, the Container protocol needs a way to refer to the type of the elements that a container will hold, without knowing what that type is for a specific container. The Container protocol needs to specify that any value passed to the append method must have the same type as the container’s element type, and that the value returned by the container’s subscript will be of the same type as the container’s element type.

To achieve this, the Container protocol declares an associated type called ItemType, written as typealias ItemType. The protocol does not define what ItemType is an alias for—that information is left for any conforming type to provide. Nonetheless, the ItemType alias provides a way to refer to the type of the items in a Container, and to define a type for use with the append method and subscript, to ensure that the expected behavior of any Container is enforced.

Here’s a version of the non-generic IntStack type from earlier, adapted to conform to the Container protocol:

    struct IntStack: Container {
    // original IntStack implementation
    var items = Int[]()
    mutating func push(item: Int) {
    items.append(item)
    }
    mutating func pop() -> Int {
    return items.removeLast()
    }
    // conformance to the Container protocol
    typealias ItemType = Int
    mutating func append(item: Int) {
    self.push(item)
    }
    var count: Int {
    return items.count
    }
    subscript(i: Int) -> Int {
    return items[i]
    }
    }

The IntStack type implements all three of the Container protocol’s requirements, and in each case wraps part of the IntStack type’s existing functionality to satisfy these requirements.

Moreover, IntStack specifies that for this implementation of Container, the appropriate ItemType to use is a type of Int. The definition of typealias ItemType = Int turns the abstract type of ItemType into a concrete type of Int for this implementation of the Container protocol.

Thanks to Swift’s type inference, you don’t actually need to declare a concrete ItemType of Int as part of the definition of IntStack. Because IntStack conforms to all of the requirements of the Container protocol, Swift can infer the appropriate ItemType to use, simply by looking at the type of the append method’s item parameter and the return type of the subscript. Indeed, if you delete the typealias ItemType = Int line from the code above, everything still works, because it is clear what type should be used for ItemType.

You can also make the generic Stack type conform to the Container protocol:

    struct Stack<T>: Container {
    // original Stack<T> implementation
    var items = T[]()
    mutating func push(item: T) {
    items.append(item)
    }
    mutating func pop() -> T {
    return items.removeLast()
    }
    // conformance to the Container protocol
    mutating func append(item: T) {
    self.push(item)
    }
    var count: Int {
    return items.count
    }
    subscript(i: Int) -> T {
    return items[i]
    }
    }

This time, the placeholder type parameter T is used as the type of the append method’s item parameter and the return type of the subscript. Swift can therefore infer that T is the appropriate type to use as the ItemType for this particular container.
Extending an Existing Type to Specify an Associated Type

You can extend an existing type to add conformance to a protocol, as described in Adding Protocol Conformance with an Extension. This includes a protocol with an associated type.

Swift’s Array type already provides an append method, a count property, and a subscript with an Int index to retrieve its elements. These three capabilities match the requirements of the Container protocol. This means that you can extend Array to conform to the Container protocol simply by declaring that Array adopts the protocol. You do this with an empty extension, as described in Declaring Protocol Adoption with an Extension:

    extension Array: Container {}

Array’s existing append method and subscript enable Swift to infer the appropriate type to use for ItemType, just as for the generic Stack type above. After defining this extension, you can use any Array as a Container.

Where Clauses

Type constraints, as described in Type Constraints, enable you to define requirements on the type parameters associated with a generic function or type.

It can also be useful to define requirements for associated types. You do this by defining where clauses as part of a type parameter list. A where clause enables you to require that an associated type conforms to a certain protocol, and/or that certain type parameters and associated types be the same. You write a where clause by placing the where keyword immediately after the list of type parameters, followed by one or more constraints for associated types, and/or one or more equality relationships between types and associated types.

The example below defines a generic function called allItemsMatch, which checks to see if two Container instances contain the same items in the same order. The function returns a Boolean value of true if all items match and a value of false if they do not.

The two containers to be checked do not have to be the same type of container (although they can be), but they do have to hold the same type of items. This requirement is expressed through a combination of type constraints and where clauses:

    func allItemsMatch<
    C1: Container, C2: Container
    where C1.ItemType == C2.ItemType, C1.ItemType: Equatable>
    (someContainer: C1, anotherContainer: C2) -> Bool {
    // check that both containers contain the same number of items
    if someContainer.count != anotherContainer.count {
    return false
    }
    // check each pair of items to see if they are equivalent
    for i in 0..someContainer.count {
    if someContainer[i] != anotherContainer[i] {
    return false
    }
    }
    // all items match, so return true
    return true
    }

This function takes two arguments called someContainer and anotherContainer. The someContainer argument is of type C1, and the anotherContainer argument is of type C2. Both C1 and C2 are placeholder type parameters for two container types to be determined when the function is called.

The function’s type parameter list places the following requirements on the two type parameters:

    C1 must conform to the Container protocol (written as C1: Container).

    C2 must also conform to the Container protocol (written as C2: Container).

    The ItemType for C1 must be the same as the ItemType for C2 (written as C1.ItemType == C2.ItemType).

    The ItemType for C1 must conform to the Equatable protocol (written as C1.ItemType: Equatable).

The third and fourth requirements are defined as part of a where clause, and are written after the where keyword as part of the function’s type parameter list.

These requirements mean:

    someContainer is a container of type C1.

    anotherContainer is a container of type C2.

    someContainer and anotherContainer contain the same type of items.

    The items in someContainer can be checked with the not equal operator (!=) to see if they are different from each other.

The third and fourth requirements combine to mean that the items in anotherContainer can also be checked with the != operator, because they are exactly the same type as the items in someContainer.

These requirements enable the allItemsMatch function to compare the two containers, even if they are of a different container type.

The allItemsMatch function starts by checking that both containers contain the same number of items. If they contain a different number of items, there is no way that they can match, and the function returns false.

After making this check, the function iterates over all of the items in someContainer with a for-in loop and the half-closed range operator (..). For each item, the function checks whether the item from someContainer is not equal to the corresponding item in anotherContainer. If the two items are not equal, then the two containers do not match, and the function returns false.

If the loop finishes without finding a mismatch, the two containers match, and the function returns true.

Here’s how the allItemsMatch function looks in action:

    var stackOfStrings = Stack<String>()
    stackOfStrings.push("uno")
    stackOfStrings.push("dos")
    stackOfStrings.push("tres")
    var arrayOfStrings = ["uno", "dos", "tres"]
    if allItemsMatch(stackOfStrings, arrayOfStrings) {
    println("All items match.")
    } else {
    println("Not all items match.")
    }
    // prints "All items match."

The example above creates a Stack instance to store String values, and pushes three strings onto the stack. The example also creates an Array instance initialized with an array literal containing the same three strings as the stack. Even though the stack and the array are of a different type, they both conform to the Container protocol, and both contain the same type of values. You can therefore call the allItemsMatch function with these two containers as its arguments. In the example above, the allItemsMatch function correctly reports that all of the items in the two containers match. 
