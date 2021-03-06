# 集合类型

Swift 提供了两种*集合类型* 来存储数据集合，分别是数组(arrays)和字典(dictionaries)。数组用来存储有序的相同类型数据的列表。字典用来存储无序的相同类型数据的集合，这些数据可以通过唯一的标识符（称为*键*）引用和查找。

在Swift中，数组和字典可以存储的键值类型总是明确的。这意味着不会把错误类型的值意外地插入到数组或字典中。这也意味着我们可以清楚的知道从数组或字典中获取的数据类型。Swift 使用显示类型集合，这确保了代码中可以处理的数据类型是明确的，并让我们可以提前发现开发中的任何类型错误。


>注意

>Swift的`Array`类型在赋值给常量、变量或传入函数和方法时与其他类型的行为稍有不同。获取更多信息请参见[Mutability of Collections](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/04_Collection_Types.md#mutability-of-collections)and[AssignmentCopy Behavior for Collection Types]()这两个章节。


## 数组

*数组*在一个有序列表中存储了多个相同类型的数据。相同的数据可以多次出现在数组的不同位置。

Swift 数组可以存储的数据类型是确定的。这与 Objective-C 的类 `NSArray` 和 `NSMutableArray` 不同，这两个类可以存储任何类型的对象，并且不会提供它们返回的对象的任何信息。在 Swift 中，某个数组可以存储的数据类型是确定的，可以使用显式的类型声明，也可以使用类型推断，且不必一定是 class 类型。假如你创建了一个 `Int` 型的数组，那么就不能在这个数组中插入其他任何非 `Int` 型的值。Swift 数组是类型安全的，并且它们可以包含的类型是明确的。
‌
### 数组类型简写语法

Swift 数组类型的完整写法是 `Array<SomeType>`, 这里的 `SomeType` 指的是数组可以存储的类型。我们也可以把它简写为 `SomeType[]`。尽管这两种形式在功能上完全相同，但更推荐简写形式，且本书中提到数组类型时都会使用这种形式。
‌
### 数组字面量

我们可以用*数组字面量*来初始化数组，这是一个或多个值作为数组集合的简写方式。数组字面量写作一个数值列表，由逗号分隔，被一对方括号括起来：

```
 [value 1, value 2, value 3]
```

下面这个例子创建了一个名为 `shoppingList` 的数组来存储 `String` 类型的数据。

```
var shoppingList: String[] = ["Eggs", "Milk"]
// 使用两个初始化项，初始化了shoppingList
```

变量shoppingList声明为“`String` 类型的数组”，写为 `String[]`。由于这个特定数组指定了 `String` 的数据类型，因此它*只能*存储 `String` 类型的数据。这里的 `shoppingList` 数组由两个`String` 值(`"Eggs" `和 `"Milk"`)以数组字面量来初始化。

>注意

>数组 `shoppingList` 声明为变量（通过关键字 `var` ）而不是常量（通过关键字 `let`），因为在下面的例子中，会有更多的数组项添加到这个购物列表中。

在这个例子中，该数组字面量只包含了两个 `String` 值。这和 `shoppingList` 变量的声明（只能包含 `String` 值的数组）是一致的，因此数组字面量的赋值作为一种方式，可以使用两个初始项初始化`shoppingList`。

多亏了 Swift 的类型推断，如果使用包含相同类型数据的数组字面量，我们不需要写出数组的类型。`shopplingList`的初始化可以简写为：

```
var shoppingList = ["Eggs", "Milk"]
```

因为数组字面量中所有的值的类型是相同的，Swift 可以推断出 `String[]` 是 `shoppingList` 变量使用的正确类型。
‌
### 访问和修改数组

我们可以通过数组的方法、属性或使用下标语法来访问和修改数组。

可以通过数组的只读属性 `count` 来获得数组包含的数组项个数。

```
println("The shopping list contains \(shoppingList.count) items.")
// 打印出 "The shopping list contains 2 items."
```

用布尔值 `isEmpty` 属性来作为检查 `count` 属性是否等于 `0` 的快捷方式。

```
if shoppingList.isEmpty {
    println("The shopping list is empty.")
} else {
    println("The shopping list is not empty.")
}
// 打印出 "The shopping list is not empty.”

```

可以通过调用数组的 `append` 方法，在数组的末尾插入一个新的数据项。

```
shoppingList.append("Flour")

// shoppingList 现在包含3项, 有人在做煎饼
```

或者，可以通过加法赋值运算符（`+=`）在数组的末尾添加新的数据项。

```
shoppingList += "Baking Powder"
// shoppingList 现在包含4项
```

你还可以通过加法赋值运算符（`+=`）插入一个同类型的数组。

```
shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
// shoppingList 现在包含7项
```

通过*下标语法*从数组中获取某个值，即在数组名后紧跟的方括号中传入想要获取的值的索引：

```
var firstItem = shoppingList[0]
// firstItem 等于 "Eggs"
```

注意，数组中第一个数组项的索引为`0`，而不是`1`。Swift数组的索引是从零开始的。

使用下标语法可以在给定的索引处改变已存在的值。

```
shoppingList[0] = "Six eggs"
// 列表中第一项现在等于 "Six eggs" ，而不是"Eggs"
```

我们还可以通过下标语法一次改变一个范围内的值，即使替换的值的集合与被替换的范围的长度不一致。下面的例子用 `"Bananas"` and `"Apples"`替换了 `"Chocolate Spread"`, `"Cheese"`, and `"Butter"`：

```
shoppingList[4...6] = ["Bananas", "Apples"]
// shoppingList现在包含6项
```

>注意

>不能使用下标语法在数组的末尾添加新的数据项。如果我们试图用一个超过数组边界的下标访问或设置某个数值时，会导致运行时错误。不过，我们可以通过比较索引和数组的 `count` 属性来判断该索引是否有效。除了 count 为`0`时（意味着这个数组是空的），数组中最大的有效索引为 `count-1`，因为数组的索引是从0开始的。

要在数组的指定索引处插入一个数组项，可以调用数组的 `insert(atIndex:)` 方法：

```
shoppingList.insert("Maple Syrup", atIndex: 0)
// shoppingList 现在包含7项
// "Maple Syrup" 现在是列表的第一项
```

这个例子调用 `insert` 方法指定索引为 `0`，在 shoppingList 的最前面插入了值为 `“Maple Syrup”` 的新数据项。

类似地，`removeAtIndex` 方法可以从数组中移除一个数组项。该方法移除指定索引处的数组项，并返回被移除的数组项（如果不需要，我们可以忽略返回值）：

```
let mapleSyrup = shoppingList.removeAtIndex(0)
// 索引为0的数据项被移除
// shoppingList 现在包含6项, 不包括 Maple Syrup
// mapleSyrup 现在等于被移除的 " Maple Syrup" 字符串
```

当一个数组项被移除后数组中的空缺项会被自动填补，因此索引`0`对应的值再次等于`“Six eggs”`:

```
firstItem = shoppingList[0]
// firstItem 现在等于"Six eggs"
```

如果我们想要从数组中移除最后一个数组项，最好使用 `removeLast` 方法，而不是 `removeAtIndex` 方法，这样可以避免查询数组的 `count` 属性。像 `removeAtIndex` 方法那样，`removeLast` 方法也会返回被移除的数组项：

```
let apples = shoppingList.removeLast()
// 数组中最后一项被移除
// shoppingList 现在包含5项, 不包括cheese
// apples 现在等于被移除的"Apples" 字符串
```

### 遍历数组
我们可以使用 `for-in` 循环来遍历数组中的所有数组项：

```
for item in shoppingList {
    println(item)
}
// Six eggs
// Milk
// Flour
// Baking Powder
// Bananas
```
如果需要每一项的整型索引及对应的值，那么可以使用全局函数 `enumerate` 来遍历数组。函数 `enumerate` 返回由每个数组项的索引和对应的值组成的元组。我们可以把元组分解为临时的常量或者变量来进行遍历。

```
for (index, value) in enumerate(shoppingList) {
    println("Item \(index + 1): \(value)")
}
// Item 1: Six eggs
// Item 2: Milk
// Item 3: Flour
// Item 4: Baking Powder
// Item 5: Bananas
```
获取更多关于 `for-in` 循环的介绍，请参见 [For循环](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/05_Control_Flow.md#for%E5%BE%AA%E7%8E%AF)。


### 创建和初始化数组

我们可以使用初始化语法来创建某一特定类型的空数组（没有设置任何初始值）：

```
var someInts = Int[]()
println("someInts is of type Int[] with \(someInts.count) items.")
// 打印出 "someInts is of type Int[] with 0 items."
```
注意，变量 `someInts` 的类型被认为是 `Int[]`，因为它设置为`Int[]`初始化器的输出结果。

或者，如果上下文已经提供了类型信息，例如一个函数参数，或一个已经指定类型的变量或常量，我们可以用空数组字面量来创建空数组，写为`[]`（一对空的方括号）：

```
someInts.append(3)
// someInts 现在包含 1 个 Int 值

someInts = []
// someInts 现在是一个空数组, 但仍然是Int[]类型
```

Swift `数组`类型还提供了一个初始化器来创建指定大小的数组，该数组的数据项设置为提供的默认值。我们把新加的数组项的大小（称为`count`）和相应类型的默认值（称为`repeatedValue`）传递给初始化器。

```
var threeDoubles = Double[](count: 3, repeatedValue: 0.0)
// threeDoubles 是 Double[] 类型，等于[0.0, 0.0, 0.0]
```
多亏有类型推导，使用初始化器时，可以不需要指定数组存储的类型，因为可以从默认值推导类型：

```
var anotherThreeDoubles = Array(count: 3, repeatedValue: 2.5)
// anotherThreeDoubles 推导为 Double[] 类型，等于 [2.5, 2.5, 2.5]
```
最后，我们可以使用加法操作符（`+`）把两个已经存在的相同类型的数组相加来创建一个新的数组。这个新数组的类型是从两个相加的数组的类型推导出来的：

```
var sixDoubles = threeDoubles + anotherThreeDoubles
// sixDoubles 推导为Double[]类型, 等于 [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```


## 字典

*字典*是存储多个相同类型数值的容器。每个值和字典中作为该值的唯一标识符的*键* (key) 相关联。和数组中的数据项不同，字典中的数据项没有顺序。我们可以使用字典根据标识符来查找数据，就像在现实世界中可以用字典来查找某个特定字词的定义。

Swift 字典存储的键和值的类型是确定的。他们和 Objective-C 的类 `NSDictionary` 和 `NSMutableDictionary` 有所不同，这些类可以用任意一种对象作为他们的键和值，且不提供这些对象本质相关的任何信息。在 Swift 中，某个字典可以存储的键和值的类型是确定的，可以使用显式类型声明，也可以使用类型推断。

Swift 字典类型写为 `Dictionary<KeyType, ValueType>`，这里的 `KeyType` 是可以作为字典键的数据类型，`ValueType` 是字典中存储的与键相对应的值的类型。

`KeyType` 的唯一限制是它必须是*可哈希的*——也就是说，它必须提供一个方法可以唯一代表自己。所有的 Swift 基础类型（如 `String`、`Int`、 `Double` 和 `Bool`）默认都是可哈希的，所有的这些类型都可以被用来作为字典的键。没有对应值的枚举成员数据（参见 [Enumerations](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/08_Enumerations.md)）默认也是可哈希的。

‌
### 字典字面量

你可以用*字典字面量*来初始化一个字典，这和之前的数组字面量有着相似的语法。字典字面量是一个或多个键-值对作为`字典`集合的简写方式。

*键-值对*是键和值的组合。在字典字面量中，每个键-值对中的键和值由冒号分隔。键值对的列表，用逗号分隔，由方括号括起来：

```
 [key 1: value 1, key 2: value 2, key 3: value 3]
 ```
下面的例子创建了一个字典来储存国际机场的名字。在这个字典中，键是由三个字母组成的国际航空运输协会代码，值是机场的名称：

```
var airports: Dictionary<String, String> = ["TYO": "Tokyo", "DUB": "Dublin"]
```
`airports`字典声明为`Dictionary<String, String>`类型，即“一个键和值的类型都是`String`类型的字典”。

>注意

>`airports`字典声明为变量（用关键字`var`），而不是常量（用关键字`let`），因为在下面的例子中，会有更多的机场被添加到这个字典里。

`airports` 字典由包含两对键值对的字典字面量初始化。第一对有键`“TYO”` 和值 `“Tokyo”`。第二对有键 `“DUB”` 和值 `“Dublin”`。

这个字典字面量包含两个 `String`：`String` 类型的键值对。这和变量 `airports` 声明（只有 `String` 键和 `String` 值的字典）的类型一致，因此字典字面量的赋值作为一种方法，可以用两个初始项来初始化这个 `airports` 字典。

和数组一样，如用我们用键值类型相同的字典字面量来初始化字典，那么不需要写出它的类型。`airports` 的初始化可以简写为以下形式：

```
var airports = ["TYO": "Tokyo", "DUB": "Dublin"]
```

由于字面量中所有的键和值都是相同类型的，因此 Swift 可以推断出 `Dictionary<String, String>` 是字典 `airports` 使用的正确类型。
‌
### 访问和修改字典

我们可以通过字典的方法和属性，或下标语法来访问和修改字典。像数组那样，我们可以通过检查只读属性 `count` 来获取`字典`中数据项的个数。

```
println("The dictionary of airports contains \(airports.count) items.")
// 打印出 "The dictionary of airports contains 2 items."

```

我们可以通过下标语法给字典添加新的数据项。使用相应类型的键作为下标索引，并赋予相应类型的值：

```
airports["LHR"] = "London"
// airports 字典现在包含3项
```

我们还可以使用下标语法改变某个键对应的值：

```
airports["LHR"] = "London Heathrow"
// "LHR" 的值修改为 "London Heathrow"
```

字典的 `updateValue(forKey:)` 方法可作为下标的替代来设置或更新某个特定键对应的值。像上面下标的例子，`updateValue(forKey:)` 方法可以设置某个不存在的键的值或者更新某个已有的键的值。和下标不同的是，`updateValue(forKey:)` 方法在更新数据后会返回更新前的数值。这使得我们可以检查更新是否成功。

`updateValue(forKey:)` 方法返回字典值类型的可选值。举个例子，对于一个储存了 `String` 数据的字典，这个方法返回了一个 `String?类型` 或“可选的 `String`”类型的数据。如果在更新之前这个键是存在的，则这个可选数据返回更新之前的值，否则返回 `nil`。

```
if let oldValue = airports.updateValue("Dublin International", forKey: "DUB") {
    println("The old value for DUB was \(oldValue).")
}
// 打印出 "The old value for DUB was Dublin."
```

我们也可以使用下标语法来访问字典中某个特定键对应的值。因为有可能会查询一个没有对应值的键，字典的下标会返回字典数据类型的可选值。如果字典包含了与要查找的键相对应的值，下标返回的可选值包含那个键对应的值，否则下标返回 `nil`。

```
if let airportName = airports["DUB"] {
    println("The name of the airport is \(airportName).")
} else {
    println("That airport is not in the airports dictionary.")
}
// 打印出 "The name of the airport is Dublin International."
```

我们可以使用下标语法设置某个指定键的值为 `nil` 来从字典中移除该键值对。

```
airports["APL"] = "Apple International"
// "Apple International" 不是APL的真实机场，所以删除它
airports["APL"] = nil
// APL 已经从字典中移除了
```

我们还可以使用 `removeValueForKey` 方法从字典中移除一个键值对。如果要移除的键对应的值对存在，该方法会移除它们并返回被移除的值，如果对应的值不存在，则返回 `nil`。

```
if let removedValue = airports.removeValueForKey("DUB") {
    println("The removed airport's name is \(removedValue).")
} else {
    println("The airports dictionary does not contain a value for DUB.")
}

//打印出 "The removed airport's name is Dublin International."
```

### 字典遍历
我们可以用 `for-in` 循环遍历一个字典中的键值对。字典中的每个数据项返回相应的(`键, 值`)元组，我们可以把元组分解为临时常量或变量用于遍历：

```
for (airportCode, airportName) in airports {
    println("\(airportCode): \(airportName)")
}
// TYO: Tokyo
// LHR: London Heathrow
```
更多关于 `for-in` 循环的介绍，请参见 [For循环](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/05_Control_Flow.md#for%E5%BE%AA%E7%8E%AF)。

可以使用字典的 `keys` 或 `values` 属性得到字典的键和值的遍历集合。

```
for airportCode in airports.keys {
    println("Airport code: \(airportCode)")
}
// Airport code: TYO
// Airport code: LHR
 
for airportName in airports.values {
    println("Airport name: \(airportName)")
}
// Airport name: Tokyo
// Airport name: London Heathrow
```

如果需要使用字典的API 生成键和值的 `Array` 实例，可以使用 `keys` 或 `values` 属性初始化新数组。

```
let airportCodes = Array(airports.keys)
// airportCodes is ["TYO", "LHR"]
 
let airportNames = Array(airports.values)
// airportNames is ["Tokyo", "London Heathrow"]
```

>注意

>Swift 字典类型是无序的集合。遍历字典时键、值以及键值对的访问顺序是不确定的。
‌

### 创建空字典

和数组一样，我们可以使用初始化语法创建一个特定类型的空 `字典`。

```
var namesOfIntegers = Dictionary<Int, String>()
// namesOfIntegers is an empty Dictionary<Int, String>

// namesOfIntegers 是一个空字典<Int, String>
```

这个例子创建了 `Int`，`String` 类型的空字典来存储整型的可读性名称。它的键的类型是 `Int`，值的类型是 `String`。

如果上下文已经提供了类型信息，可以用空字典字面量来创建空字典，写为[`:`] (中括号中放一个冒号)：

```
namesOfIntegers[16] = "sixteen"
// namesOfIntegers 现在包含1个键-值对

namesOfIntegers = [:]
// namesOfIntegers再一次成为 Int, String 类型的空字典
```

>注意

>在后台，Swift 数组和字典类型都是由*泛型集合*实现的。更多关于泛型类型和集合的介绍，请参见 [Generics](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/22_Generics.md)。
‌

## 集合的易变性

数组和字典在单个集合中存储了多个数据。如果我们创建一个数组或字典并把它声明为变量，这个创建出来的集合是*易变的*。这意味着我们可以改变集合的大小，在集合中添加更多的数据项，或从中移除已有的数据项。相反的，如果把一个数组或字典声明为常量，则这个数组或字典是*不可变*的，它的大小是不会变化的。

对字典来说，不可变还意味着我们不能替换字典中某个已有的键对应的值。一个不可变字典的内容一旦设置就不能再改变。

对数组来说，不可变的意义稍有不同。我们仍不允许改变不可变数组的大小，但是，我们*被*允许改变数组中某个已有索引对应的值。这使得 Swift 的 `Array` 类型可以在操作固定大小的数组时提供最佳性能。

Swift 的 `Array` 类型的可变性还会影响数组实例如何赋值和修改。更多介绍请参见 [集合类型的声明和复制](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/09_Classes_and_Structures.md#%E9%9B%86%E5%90%88%E7%9A%84%E8%B5%8B%E5%80%BC%E4%B8%8E%E6%8B%B7%E8%B4%9D)。

>注意
>当集合的大小不需要改变时，创建一个不可变的集合是比较好的做法。这样做，Swift 编译器会优化创建的集合性能。


