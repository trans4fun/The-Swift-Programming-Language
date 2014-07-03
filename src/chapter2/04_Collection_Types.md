# Collection Types
# 集合类型

Swift provides two *collection types*, known as arrays and dictionaries, for storing collections of values. Arrays store ordered lists of values of the same type. Dictionaries store unordered collections of values of the same type, which can be referenced and looked up through a unique identifier (also known as a *key*).

Swift提供了两种*集合类型* 来存储数据集合，分别是数组(arrays)和词典(dictionaries)。数组用来存储有序的相同类型数据的列表。字典用来存储无序的相同类型的数据的集合，这些数据可以通过一个唯一的标识符（称为*键*）来引用和查找。

Arrays and dictionaries in Swift are always clear about the types of values and keys that they can store. This means that you cannot insert a value of the wrong type into an array or dictionary by mistake. It also means you can be confident about the types of values you will retrieve from an array or dictionary. Swift’s use of explicitly typed collections ensures that your code is always clear about the types of values it can work with and enables you to catch any type mismatches early in your code’s development.

在Swift中，数组和词典能够存储的键值类型一直是很明确的。这意味着我们不能错误地把类型不正确的数据插入到一个数组或词典中。这也意味着我们能够清楚的知道从一个数组或词典中获取到的数据的类型。Swift的显式类型的集合使得我们清楚代码中能够处理哪种类型的数据，并使得我们可以更早的在代码开发过程中发现任何类型错误。

>NOTE

>Swift’s `Array` type exhibits different behavior to other types when assigned to a constant or variable, or when passed to a function or method. For more information, see [Mutability of Collections](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/04_Collection_Types.md#mutability-of-collections) and [Assignment and Copy Behavior for Collection Types]().

>注意

>Swift的`Array`类型在赋值给常量和变量，还有传入函数和方法时与其他类型有所不同。获取更多信息请参见[Mutability of Collections](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/04_Collection_Types.md#mutability-of-collections)and[AssignmentCopy Behavior for Collection Types]()这两个章节。


## Arrays
## 数组
An *array* stores multiple values of the same type in an ordered list. The same value can appear in an array multiple times at different positions.

*数组*在一个有序列表中存储了多个相同类型的数据。相同的数据可以多次出现在数组的不同位置。

Swift arrays are specific about the kinds of values they can store. They differ from Objective-C’s `NSArray` and `NSMutableArray` classes, which can store any kind of object and do not provide any information about the nature of the objects they return. In Swift, the type of values that a particular array can store is always made clear, either through an explicit type annotation, or through type inference, and does not have to be a class type. If you create an array of `Int` values, for example, you can’t insert any value other than `Int` values into that array. Swift arrays are type safe, and are always clear about what they may contain.

Swift数组能够存储的数据类型是确定的。这与Objective-C的类`NSArray`和`NSMutableArray`是不同的，这两个类能够存储任何一种类型的对象，并且不会提供它们返回的对象的任何信息。在Swift中，某个数组能够存储的数据类型是确定的，不是通过显式的类型声明，就是通过类型推断，不需要为class类型。假我们你创建了一个`Int`型的数组，那么就不能插入其他任何非`Int`型的值到这个数组中。Swift数组是类型安全的，并且它们能够包含的值也是明确的。
‌
### Array Type Shorthand Syntax
### 数组类型缩写语法
The type of a Swift array is written in full as `Array<SomeType>`, where `SomeType` is the type that the array is allowed to store. You can also write the type of an array in shorthand form as `SomeType[]`. Although the two forms are functionally identical, the shorthand form is preferred, and is used throughout this guide when referring to the type of an array.

Swift数组的类型的完整写法是`Array<SomeType>`, 这里的`SomeType`指的是数组能够存储的类型。我们也可以把它缩写为`SomeType[]`。这两种形式的数组在功能上完全相同，不过建议使用缩写的形式，本书中提到数组类型时都会以这种形式表示。
‌
### Array Literals
### 数组字面量

You can initialize an array with an *array literal*, which is a shorthand way to write one or more values as an array collection. An array literal is written as a list of values, separated by commas, surrounded by a pair of square brackets:

你可以用*数组字面量*来初始化数组，这是把一个或多个值作为数组集合的缩写方式。数组字面量被写作一个数值列表，由逗号分隔开来，被一对方括号括起来：

```
 [value 1, value 2, value 3]
```
 
The example below creates an array called `shoppingList` to store `String` values:

下面这个例子创建了一个命名为`shoppingList`的数组来存储`String`类型的数据。

```
var shoppingList: String[] = ["Eggs", "Milk"]
// shoppingList has been initialized with two initial items
```

The `shoppingList` variable is declared as “an array of `String` values”, written as `String[]`. Because this particular array has specified a value type of `String`, it is *only* allowed to store `String` values. Here, the `shoppingList` array is initialized with two `String` values (`"Eggs" `and `"Milk"`), written within an array literal.

变量shoppingList被声明为“一个`String`类型的数组”，写为`String[]`。这个特定数组的类型确定为`String`，因此它*只能*存储`String`类型的数据。这里的`shoppingList`数组被写在一个数组字面量中的两个`String`值（`“Egg”`和`"Milk"`）初始化。

>NOTE

>The `shoppingList` array is declared as a variable (with the `var` introducer) and not a constant (with the `let` introducer) because more items are added to the shopping list in the examples below.

>注意

>数组`shoppingList`被声明为变量（通过关键字`var`）而不是常量（通过关键字`let`），因为在下面的例子中，更多的数组项被添加到这个购物列表中。

In this case, the array literal contains two `String `values and nothing else. This matches the type of the `shoppingList` variable’s declaration (an array that can only contain `String` values), and so the assignment of the array literal is permitted as a way to initialize `shoppingList` with two initial items.

在这个例子中，该数组字面量只包含了两个`String`值。这和shoppingList变量的声明（只能包含`String`值的数组）是一致的，因此数组字面量的赋值被用来作为一种用两个初始项来初始化shopplingList的方式。

Thanks to Swift’s type inference, you don’t have to write the type of the array if you’re initializing it with an array literal containing values of the same type. The initialization of `shoppingList` could have been written in a shorter form instead:

感谢Swift的类型推断，通过包含相同类型数据的数组字面量，我们不需要去写正在初始化的数组的类型。`shopplingList`的初始化可以缩写为：

```
var shoppingList = ["Eggs", "Milk"]
```

Because all values in the array literal are of the same type, Swift can infer that `String[]` is the correct type to use for the `shoppingList` variable.

因为数组字面量中所有的值的类型是相同的，Swift能够推断出`String[]`是`shoppingList`变量使用的正确类型。
‌
### Accessing and Modifying an Array
### 获取和修改数组
You access and modify an array through its methods and properties, or by using subscript syntax.

我们可以通过数组的方法、属性或下标语法来访问和修改数组。

To find out the number of items in an array, check its read-only `count` property:

可以通过数组的只读属性`count`来获得数组包含的数组项个数，。

```
println("The shopping list contains \(shoppingList.count) items.")
// prints "The shopping list contains 2 items."
```

Use the Boolean `isEmpty` property as a shortcut for checking whether the `count` property is equal to `0`:

用布尔值`isEmpty`属性来作为查看`count`属性是否等于`0`的快捷方式。

```
if shoppingList.isEmpty {
    println("The shopping list is empty.")
} else {
    println("The shopping list is not empty.")
}
// prints "The shopping list is not empty.”
```

You can add a new item to the end of an array by calling the array’s `append` method:

我们可以通过调用数组的`append`方法来插入一个新的数组项到数组的末尾。

```
shoppingList.append("Flour")
// shoppingList now contains 3 items, and someone is making pancakes
```

Alternatively, add a new item to the end of an array with the addition assignment operator (`+=`):

或者，可以通过加法赋值运算符（`+=`）来添加新的数组项到数组的末尾。

```
shoppingList += "Baking Powder"
// shoppingList now contains 4 items
```

You can also append an array of compatible items with the addition assignment operator (`+=`):

你还可以通过加法赋值运算符（`+=`）来插入一个同类型的数组。

```
shoppingList += ["Chocolate Spread", "Cheese", "Butter"]
// shoppingList now contains 7 items
```

Retrieve a value from the array by using *subscript syntax*, passing the index of the value you want to retrieve within square brackets immediately after the name of the array:

通过*下标语法*从数组中获取某个值，即在数组名之后紧跟由方括号括起来的想要获取的值的索引：

```
var firstItem = shoppingList[0]
// firstItem is equal to "Eggs"
```

Note that the first item in the array has an index of `0`, not `1`. Arrays in Swift are always zero-indexed.

注意，数组中第一个数组项的索引为`0`，而不是`1`。Swift数组的索引是从零开始的。

You can use subscript syntax to change an existing value at a given index:

通过指定的索引，我们可以使用下标语法来修改一个已经存在的值：

```
shoppingList[0] = "Six eggs"
// the first item in the list is now equal to "Six eggs" rather than "Eggs"
```

You can also use subscript syntax to change a range of values at once, even if the replacement set of values has a different length than the range you are replacing. The following example replaces `"Chocolate Spread"`, `"Cheese"`, and `"Butter"` with `"Bananas"` and `"Apples"`:

我们还可以通过下标语法一次改变一个范围内的值，即使要替换的值的长度和被替换的值的长度不一致。下面的例子用`"Bananas"` and `"Apples"`替换了`"Chocolate Spread"`, `"Cheese"`, and `"Butter"`：

```
shoppingList[4...6] = ["Bananas", "Apples"]
// shoppingList now contains 6 items
```

>NOTE

>You can’t use subscript syntax to append a new item to the end of an array. If you try to use subscript syntax to retrieve or set a value for an index that is outside of an array’s existing bounds, you will trigger a runtime error. However, you can check that an index is valid before using it, by comparing it to the array’s `count` property. Except when `count` is `0` (meaning the array is empty), the largest valid index in an array will always be `count - 1`, because arrays are indexed from zero.”

>注意

>我们不能使用下标语法插入一个新的数组项到数组的末尾。如果我们试图用一个超过数组边界的下标访问或设置某个数值时，会导致运行时错误。不过，我们可以通过比较索引和数组的`count`属性来判断该索引是否有效。数组中最大的有效索引为`count-1`，除了count为`0`时（意味着这个数组是空的），因为数组的索引是从0开始的。


To insert an item into the array at a specified index, call the array’s `insert(atIndex:)` method:

要给数组的指定索引处插入一个数组项，可以调用数组的`insert(atIndex:)`方法：

```
shoppingList.insert("Maple Syrup", atIndex: 0)
// shoppingList now contains 7 items
// "Maple Syrup" is now the first item in the list
```

This call to the `insert` method inserts a new item with a value of `"Maple Syrup"` at the very beginning of the shopping list, indicated by an index of `0`.

上面的例子中，调用了`insert`方法插入了一个值为`“Maple Syrup”`的新数组项到数组的开头，用索引`0`来表示。

Similarly, you remove an item from the array with the `removeAtIndex` method. This method removes the item at the specified index and returns the removed item (although you can ignore the returned value if you do not need it):

相同地，`removeAtIndex`方法可以从数组中移除一个数组项。该方法移除指定索引的数组项，并返回被移除的数组项（如果不需要，我们可以忽略返回的值）：

```
let mapleSyrup = shoppingList.removeAtIndex(0)
// the item that was at index 0 has just been removed
// shoppingList now contains 6 items, and no Maple Syrup
// the mapleSyrup constant is now equal to the removed" Maple Syrup" string
```

Any gaps in an array are closed when an item is removed, and so the value at index `0` is once again equal to `"Six eggs"`:

当一个数组项被移除后数组中的空出项会被自动填补，因此索引`0`对应的值再次等于`“Six eggs”`:

```
firstItem = shoppingList[0]
// firstItem is now equal to "Six eggs"
```
If you want to remove the final item from an array, use the `removeLast` method rather than the `removeAtIndex `method to avoid the need to query the array’s `count` property. Like the `removeAtIndex` method, `removeLast` returns the removed item:

如果我们想要从数组中移除最后一个数组项，最好使用`removeLast`方法，而不是`removeAtIndex`方法，这样能够避免去查询数组的`count`属性。像`removeAtIndex`方法那样，`removeLast`方法也会返回被移除的数组项：

```
let apples = shoppingList.removeLast()
// the last item in the array has just been removed
// shoppingList now contains 5 items, and no cheese
// the apples constant is now equal to the removed "Apples" string
```

### Iterating Over an Array
### 遍历数组
You can iterate over the entire set of values in an array with the `for-in` loop:

我们可以使用`for-in`循环来遍历数组中的所有数组项：

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
If you need the integer index of each item as well as its value, use the global `enumerate` function to iterate over the array instead. The `enumerate` function returns a tuple for each item in the array composed of the index and the value for that item. You can decompose the tuple into temporary constants or variables as part of the iteration:

如果我们除了需要每个数组项的值之外，还需要每个数组项的索引，那么可以使用全局函数`enumerate`来遍历数组。函数`enumerate`返回由每个数组项的索引和对应的值组成的元组。我们可以把元组分解为临时的常量或者变量来进行遍历。

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
For more about the `for-in` loop, see [For Loops](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/05_Control_Flow.md#for%E5%BE%AA%E7%8E%AF).

获取更多关于`for-in`循环的介绍，请参见[For循环](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/05_Control_Flow.md#for%E5%BE%AA%E7%8E%AF)。


### Creating and Initializing an Array
### 创建和初始化数组
You can create an empty array of a certain type (without setting any initial values) using initializer syntax:

我们可以使用初始化语法来创建某一特定类型的空数组（没有设置任何初始值）：

```
var someInts = Int[]()
println("someInts is of type Int[] with \(someInts.count) items.")
// prints "someInts is of type Int[] with 0 items."
```
Note that the type of the `someInts` variable is inferred to be `Int[]`, because it is set to the output of an `Int[]` initializer.

注意，变量`someInts`的类型被认为是`Int[]`，因为它的设置自于`Int[]`初始化的输出。

Alternatively, if the context already provides type information, such as a function argument or an already-typed variable or constant, you can create an empty array with an empty array literal, which is written as `[]` (an empty pair of square brackets):

或者，如果上下文已经提供了类型信息，例如一个函数参数，或一个已经指定类型的变量或常量，我们可以用空数组字面量来创建空数组，写为`[]`（一对空的方括号）：

```
someInts.append(3)
// someInts now contains 1 value of type Int
someInts = []
// someInts is now an empty array, but is still of type Int[]
```
Swift’s `Array` type also provides an initializer for creating an array of a certain size with all of its values set to a provided default value. You pass this initializer the number of items to be added to the new array (called `count`) and a default value of the appropriate type (called `repeatedValue`):

Swift`数组`类型还提供了一个构造器来创建指定大小的数组，该数组的数组项的值是默认的。我们传递给构造器新加的数组项的大小（称为`count`），以及适合类型的默认值（称为`repeatedValue`）。

```
var threeDoubles = Double[](count: 3, repeatedValue: 0.0)
// threeDoubles is of type Double[], and equals [0.0, 0.0, 0.0]
```
Thanks to type inference, you don’t need to specify the type to be stored in the array when using this initializer, because it can be inferred from the default value:

感谢类型推导，我们在使用构造器时不需要指定数组中数值的具体类型，因为类型可以从默认值中推导出来：

```
var anotherThreeDoubles = Array(count: 3, repeatedValue: 2.5)
// anotherThreeDoubles is inferred as Double[], and equals [2.5, 2.5, 2.5]
```
Finally, you can create a new array by adding together two existing arrays of compatible type with the addition operator (`+`). The new array’s type is inferred from the type of the two arrays you add together:

最后，我们可以使用加法操作符（`+`）把两个已经存在的相同类型的数组相加来创建一个新的数组。这个新数组的类型是从两个相加的数组的类型推导出来的：

```
var sixDoubles = threeDoubles + anotherThreeDoubles
// sixDoubles is inferred as Double[], and equals [0.0, 0.0, 0.0, 2.5, 2.5, 2.5]
```


## Dictionaries
## 字典
A *dictionary* is a container that stores multiple values of the same type. Each value is associated with a unique *key*, which acts as an identifier for that value within the dictionary. Unlike items in an array, items in a dictionary do not have a specified order. You use a dictionary when you need to look up values based on their identifier, in much the same way that a real-world dictionary is used to look up the definition for a particular word.

*字典*是存储多重相同类型数值的容器。每个值和字典中作为值的唯一标识符的*键*(key)相关联。和数组中的数据项不同，字典中的数据项没有顺序。我们可以使用字典查找基于标识符的数据，就像在现实世界中可以用字典来查找某个特定字词的定义。

Swift dictionaries are specific about the types of keys and values they can store. They differ from Objective-C’s `NSDictionary` and `NSMutableDictionary` classes, which can use any kind of object as their keys and values and do not provide any information about the nature of these objects. In Swift, the type of keys and values that a particular dictionary can store is always made clear, either through an explicit type annotation or through type inference.

Swift字典能够存储的键和值的类型是确定的。他们和Objective-C的类`NSDictionary`和`NSMutableDictionary`有所不同，这些类能够用任意一种对象作为他们的键和值，且不提供这些对象本质相关的任何信息。在Swift中，确定的字典能够存储的键和值的类型是确定的，要么通过显示的类型声明而来，要么通过类型推断而来。

Swift’s dictionary type is written as `Dictionary<KeyType, ValueType>`, where `KeyType` is the type of value that can be used as a dictionary key, and `ValueType` is the type of value that the dictionary stores for those keys.

Swift字典类型被写为`Dictionary<KeyType, ValueType>`，这里的`KeyType`是能够被作为字典键的数据的类型，`ValueType`是字典中存储的与键相关联的数据的类型。

The only restriction is that `KeyType` must be *hashable*—that is, it must provide a way to make itself uniquely representable. All of Swift’s basic types (such as `String`, `Int`, `Double`, and `Bool`) are hashable by default, and all of these types can be used as the keys of a dictionary. Enumeration member values without associated values (as described in [Enumerations](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/08_Enumerations.md)) are also hashable by default.

`KeyType`的唯一限制是它必须是*可哈希的*——也就是说，它必须提供一个方法来使得自己能够被唯一表示。所有的Swift基础类型（如`String`, `Int`, `Double`, 和`Bool`）默认都是可哈希的，所有的这些类型都能够被用来作为字典的键。没有关联数值的枚举类型（参见[Enumerations](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/08_Enumerations.md)）也是默认可枚举的。

‌
### Dictionary Literals
### 字典字面量
You can initialize a dictionary with a *dictionary literal*, which has a similar syntax to the array literal seen earlier. A dictionary literal is a shorthand way to write one or more key-value pairs as a `Dictionary` collection.

你可以用*字典字面量*来初始化一个字典，这个和之前的数组字面量有着相似的语法。一个字典字面量是一个缩写的方式来表示作为`字典`集合的一个或多个键值对。

A *key-value pair* is a combination of a key and a value. In a dictionary literal, the key and value in each key-value pair are separated by a colon. The key-value pairs are written as a list, separated by commas, surrounded by a pair of square brackets:

一个*键-值对*是键和值的组合。在字典字面量中，每个键-值对中的键和值由冒号分隔开来。键值对被写作一个列表，用逗号隔开，由方括号括起来：

```
 [key 1: value 1, key 2: value 2, key 3: value 3]
 ```
The example below creates a dictionary to store the names of international airports. In this dictionary, the keys are three-letter International Air Transport Association codes, and the values are airport names:

下面的例子创建了一个字典来储存国际机场的名字。在这个字典中，键是由三个字母组成的国际航空运输协会代码，值是机场的名称：

```
var airports: Dictionary<String, String> = ["TYO": "Tokyo", "DUB": "Dublin"]
```
The `airports` dictionary is declared as having a type of `Dictionary<String, String>`, which means “a `Dictionary` whose keys are of type `String`, and whose values are also of type `String`”.

`airports`字典被声明为`Dictionary<String, String>`类型，即“一个键和值的类型都是`String`类型的字典”。

>NOTE

>The `airports` dictionary is declared as a variable (with the `var` introducer), and not a constant (with the `let` introducer), because more airports will be added to the dictionary in the examples below.

>注意

>`airports`字典被声明为变量（用关键字`var`），而不是常量（用关键字`let`），因为在下面的例子中，会有更多的机场被添加到这个字典里。

The `airports` dictionary is initialized with a dictionary literal containing two key-value pairs. The first pair has a key of `"TYO"` and a value of `"Tokyo"`. The second pair has a key of `"DUB"` and a value of `"Dublin"`.

`airports`字典由包含两对键值对的字典字面量初始化。第一对有一个键`“TYO”`和一个值`“Tokyo”`。第二对有一个键`“DUB”`和一个值`“Dublin”`。

This dictionary literal contains two `String`: `String` pairs. This matches the type of the `airports` variable declaration (a dictionary with only `String` keys, and only `String` values) and so the assignment of the dictionary literal is permitted as a way to initialize the `airports` dictionary with two initial items.

这个字典字面量包含两个`String`：`String`类型的键值对。这和变量`airports`声明（只有`String`键和`String`值的字典）的类型一致，因此字典字面量的赋值被用来作为一种初始化方法来用两个初始项构建这个`airports`字典。

As with arrays, you don’t have to write the type of the dictionary if you’re initializing it with a dictionary literal whose keys and values have consistent types. The initialization of `airports` could have been be written in a shorter form instead:

像数组那样，如用我们用键值类型相同的字典字面量来初始化字典，那么我们不需要写出它的类型。`airports`的初始化可以被简写为以下形式：

```
var airports = ["TYO": "Tokyo", "DUB": "Dublin"]
```
Because all keys in the literal are of the same type as each other, and likewise all values are of the same type as each other, Swift can infer that `Dictionary<String, String>` is the correct type to use for the `airports` dictionary.
由于字面量中的键和值都是相同类型的，因而Swift能够推断出`Dictionary<String, String>` 是使用字典`airports`的正确类型。
‌
### Accessing and Modifying a Dictionary
You access and modify a dictionary through its methods and properties, or by using subscript syntax. As with an array, you can find out the number of items in a `Dictionary` by checking its read-only `count` property:

我们能够通过字典的方法和属性，以及下标语法来访问和修改字典。像数组那样，我们可以通过查询只读属性`count`来得到一个`字典`中数据项的数量。

```
println("The dictionary of airports contains \(airports.count) items.")
// prints "The dictionary of airports contains 2 items."
```
You can add a new item to a dictionary with subscript syntax. Use a new key of the appropriate type as the subscript index, and assign a new value of the appropriate type:

我们可以通过下标语法给字典添加新的数据项。使用合适类型的键作为下标索引，赋予合适类型的值：

```
airports["LHR"] = "London"
// the airports dictionary now contains 3 items
```

You can also use subscript syntax to change the value associated with a particular key:

我们还可以使用下标语法来改变和某个特定键相关联的值：

```
airports["LHR"] = "London Heathrow"
// the value for "LHR" has been changed to "London Heathrow"
```
As an alternative to subscripting, use a dictionary’s `updateValue(forKey:)` method to set or update the value for a particular key. Like the subscript examples above, the `updateValue(forKey:)` method sets a value for a key if none exists, or updates the value if that key already exists. Unlike a subscript, however, the `updateValue(forKey:)` method returns the old value after performing an update. This enables you to check whether or not an update took place.

字典的`updateValue(forKey:)`方法可作为下标的替代来设置或更新某个特定键相关联的值。像上面下标的那个例子，`updateValue(forKey:)`方法可以设置某个不存在的键的值或者更新某个已有的键的值。和下标不同的是，`updateValue(forKey:)`方法在更新数据后会返回更新之前的数值。这使得我们可以检查更新是否成功。

The `updateValue(forKey:)` method returns an optional value of the dictionary’s value type. For a dictionary that stores `String` values, for example, the method returns a value of type `String?`, or “optional `String`”. This optional value contains the old value for that key if one existed before the update, or `nil` if no value existed:

`updateValue(forKey:)`方法返回字典值类型的可选值。举个例子，对于一个储存了`String`数据的字典，这个方法返回了一个`String?类型`或“可选的`String`”类型的数据。如果在更新之前这个键是存在的，则这个可选数据返回更新之前的值，否则返回`nil`。

```
if let oldValue = airports.updateValue("Dublin International", forKey: "DUB") {
    println("The old value for DUB was \(oldValue).")
}
// prints "The old value for DUB was Dublin."
```
You can also use subscript syntax to retrieve a value from the dictionary for a particular key. Because it is possible to request a key for which no value exists, a dictionary’s subscript returns an optional value of the dictionary’s value type. If the dictionary contains a value for the requested key, the subscript returns an optional value containing the existing value for that key. Otherwise, the subscript returns `nil`:

我们也可以使用下标语法来访问一个字典中某个特定键对应的值。因为查询某个不存在对应值的键也是有可能的，字典的下标会返回字典数据类型的可选值。如果字典包含了与要查找的键相对应的值，下标返回的可选值包含那个键对应的值，否则下标返回`nil`。

```
if let airportName = airports["DUB"] {
    println("The name of the airport is \(airportName).")
} else {
    println("That airport is not in the airports dictionary.")
}
// prints "The name of the airport is Dublin International."
```
You can use subscript syntax to remove a key-value pair from a dictionary by assigning a value of `nil` for that key:

我们可以使用下标语法设置某个指定键的值为`nil`来从字典中移除该键值对。

```
airports["APL"] = "Apple International"
// "Apple International" is not the real airport for APL, so delete it
airports["APL"] = nil
// APL has now been removed from the dictionary
```

Alternatively, remove a key-value pair from a dictionary with the `removeValueForKey` method. This method removes the key-value pair if it exists and returns the removed value, or returns `nil` if no value existed:

我们还可以使用`removeValueForKey`方法从字典中移除一个键值对。如果要移除的键对应的值对存在，该方法会移除它们并返回被移除的值，如果对应的值不存在，则返回`nil`。

```
if let removedValue = airports.removeValueForKey("DUB") {
    println("The removed airport's name is \(removedValue).")
} else {
    println("The airports dictionary does not contain a value for DUB.")
}
// prints "The removed airport's name is Dublin International.
```

### Iterating Over a Dictionary
### 字典遍历
You can iterate over the key-value pairs in a dictionary with a `for-in` loop. Each item in the dictionary is returned as a (`key, value`) tuple, and you can decompose the tuple’s members into temporary constants or variables as part of the iteration:

我们可以用`for-in`循环遍历一个字典中的键值对。字典中的每个数据项返回相应的(`键, 值`)原则，我们可以把元组分解为临时常量或变量用于遍历：

```
for (airportCode, airportName) in airports {
    println("\(airportCode): \(airportName)")
}
// TYO: Tokyo
// LHR: London Heathrow
```
For more about the `for-in` loop, see [For Loops](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/05_Control_Flow.md#for%E5%BE%AA%E7%8E%AF).

更多关于`for-in`循环的介绍，请参见[For循环](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/05_Control_Flow.md#for%E5%BE%AA%E7%8E%AF)。

You can also retrieve an iteratable collection of a dictionary’s  keys or values by accessing its `keys` and `values` properties:

我们还能够通过字典的`keys`或`values`属性来遍历字典的键或值。

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

If you need to use a dictionary’s keys or values with an API that takes an `Array` instance, initialize a new array with the `keys` or `values` property:

如果我们需要使用一个使用字典的键和值，并用`Array`实例作为参数的接口，可以用`keys`或`values`属性来初始化一个新的数组。

```
let airportCodes = Array(airports.keys)
// airportCodes is ["TYO", "LHR"]
 
let airportNames = Array(airports.values)
// airportNames is ["Tokyo", "London Heathrow"]
```
>NOTE

>Swift’s Dictionary type is an unordered collection. The order in which keys, values, and key-value pairs are retrieved when iterating over a dictionary is not specified.

>注意

>Swift字典类型是无序的集合。遍历字典时键、值以及键值对的访问顺序是不确定的。
‌

### Creating an Empty Dictionary
### 创建空字典
As with arrays, you can create an empty `Dictionary` of a certain type by using initializer syntax:

如同字典，我们可以使用初始化语法创建一个特定类型的空`字典`。

```
var namesOfIntegers = Dictionary<Int, String>()
// namesOfIntegers is an empty Dictionary<Int, String>
```
This example creates an empty dictionary of type `Int`, `String` to store human-readable names of integer values. Its keys are of type `Int`, and its values are of type `String`.

这个例子创建了`Int`，`String`类型的空字典来存储整型数据的可读性名称。它的键的类型是`Int`，值的类型是`String`。

If the context already provides type information, create an empty dictionary with an empty dictionary literal, which is written as [`:`] (a colon inside a pair of square brackets):

如果上下文已经提供了类型信息，可以用空字典字面量来创建空字典，写为[`:`] (中括号中放一个冒号)：

```
namesOfIntegers[16] = "sixteen"
// namesOfIntegers now contains 1 key-value pair
namesOfIntegers = [:]
// namesOfIntegers is once again an empty dictionary of type Int, String
```

>NOTE

>Behind the scenes, Swift’s array and dictionary types are implemented as *generic collections*. For more on generic types and collections, see [Generics](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/22_Generics.md).

>注意

>在后台，Swift数组和字典类型都是由*泛型集合*实现的。更多关于泛型类型和集合的介绍，请参见[Generics](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/22_Generics.md)。

‌
## Mutability of Collections
## 集合的易变性

Arrays and dictionaries store multiple values together in a single collection. If you create an array or a dictionary and assign it to a variable, the collection that is created will be *mutable*. This means that you can change (or *mutate*) the size of the collection after it is created by adding more items to the collection, or by removing existing items from the ones it already contains. Conversely, if you assign an array or a dictionary to a constant, that array or dictionary is *immutable*, and its size cannot be changed.

数组和字典在单个集合中存储了多个数据。如果我们创建一个数组或字典并把它声明为变量，这个被创建出来的集合是*易变的*。这表示我们能够在创建集合之后通过添加更多的数据项到集合中或从中移除现有的数据项来*改变*它的大小。相反的，如果把一个数组或字典声明为常量，则这个数组或字典是*不可变*的，它的大小是不会变化的。

For dictionaries, immutability also means that you cannot replace the value for an existing key in the dictionary. An immutable dictionary’s contents cannot be changed once they are set.

对字典来说，不可变还意味着我们不能替换字典中某个现有的键对应的值。一个不可变字典的内容一旦被设置就不能再被改变。

Immutability has a slightly different meaning for arrays, however. You are still not allowed to perform any action that has the potential to change the size of an immutable array, but you *are* allowed to set a new value for an existing index in the array. This enables Swift’s `Array` type to provide optimal performance for array operations when the size of an array is fixed.

对数组来说，不可变的意义稍有不同。我们仍不允许有改变不可变数组的大小的行为，但是，我们*被*允许改变数组中某个现有索引对应的值。这使得Swift的`Array`类型能够在操作固定大小的数组时提供最佳性能。

The mutability behavior of Swift’s `Array` type also affects how array instances are assigned and modified. For more information, see [Assignment and Copy Behavior for Collection Types](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/09_Classes_and_Structures.md#assignment-and-copy-behavior-for-collection-types).

Swift的`Array`类型的可变性还影响了数组实例是怎么被声明和修改的。更多介绍请参见[集合类型的声明和复制](https://github.com/trans4fun/The-Swift-Programming-Language/blob/master/src/chapter2/09_Classes_and_Structures.md#%E9%9B%86%E5%90%88%E7%9A%84%E8%B5%8B%E5%80%BC%E4%B8%8E%E6%8B%B7%E8%B4%9D)。

>NOTE

>It is good practice to create immutable collections in all cases where the collection’s size does not need to change. Doing so enables the Swift compiler to optimize the performance of the collections you create.

>注意
>当集合的大小不需要改变时，创建一个不可变的集合是比较好的做法。这样做使得Swift编译器优化我们创建的集合的性能。


