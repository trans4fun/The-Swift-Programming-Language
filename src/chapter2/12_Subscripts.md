# Subscripts
# 下标 (Subscripts)

Classes, structures, and enumerations can define subscripts, which are shortcuts for accessing the member elements of a collection, list, or sequence. You use subscripts to set and retrieve values by index without needing separate methods for setting and retrieval. For example, you access elements in an Array instance as someArray[index] and elements in a Dictionary instance as someDictionary[key].

下标可以定义在类(Class)、结构体(structures)和枚举(enumerations)这些目标中，可以认为是访问对象、集合或序列的快捷方式。举例来说，用下标访问一个数组(Array)实例中的元素可以这样写 `someArray[index]` ，访问字典(Dictionary)实例中的元素可以这样写 `someDictionary[key]`，而不需要再调用实例的某个方法来获得元素的值。

You can define multiple subscripts for a single type, and the appropriate subscript overload to use is selected based on the type of index value you pass to the subscript. Subscripts are not limited to a single dimension, and you can define subscripts with multiple input parameters to suit your custom type’s needs.

对于同一个目标可以定义多个下标，通过索引值类型的不同来进行重载，而且索引值的个数可以是多个。

> 译者：这里下标重载在本小节中原文并没有任何演示

## Subscript Syntax
## 下标语法

Subscripts enable you to query instances of a type by writing one or more values in square brackets after the instance name. Their syntax is similar to both instance method syntax and computed property syntax. You write subscript definitions with the subscript keyword, and specify one or more input parameters and a return type, in the same way as instance methods. Unlike instance methods, subscripts can be read-write or read-only. This behavior is communicated by a getter and setter in the same way as for computed properties:

下标允许你通过在实例后面的方括号中传入一个或者多个的索引值来对实例进行访问和赋值。语法类似于实例方法和实例属性的混合。与定义实例方法类似，定义下标使用`subscript`关键字，显式声明入参（一个或多个）和返回类型。与实例方法不同的是下标可以设定为读写或只读。这种方式又有点像实例属性的getter和setter：

```
subscript(index: Int) -> Int {
    get {
        // return an appropriate subscript value here
    }
    set(newValue) {
        // perform a suitable setting action here
    }
}
```

```
subscript(index: Int) -> Int {
	get {
		// 返回与入参匹配的Int类型的值
	}

	set(newValue) {
		// 执行赋值操作
	}
}
```

The type of newValue is the same as the return value of the subscript. As with computed properties, you can choose not to specify the setter’s (newValue) parameter. A default parameter called newValue is provided to your setter if you do not provide one yourself.

`newValue`的类型必须和下标定义的返回类型相同。与实例属性相同的是set的入参声明`newValue`就算不写，在set代码块中依然可以使用`newValue`这个变量来访问新赋的值。

As with read-only computed properties, you can drop the get keyword for read-only subscripts:

与只读实例属性一样，可以直接将原本应该写在get代码块中的代码写在subscript中即可：

```
subscript(index: Int) -> Int {
    // return an appropriate subscript value here
}
```

```
subscript(index: Int) -> Int {
	// 返回与入参匹配的Int类型的值
}
```

Here’s an example of a read-only subscript implementation, which defines a TimesTable structure to represent an n-times-table of integers:

下面代码演示了一个在TimesTable结构体中使用只读下标的用法，该结构体用来展示传入整数的N倍。

```
struct TimesTable {
    let multiplier: Int
    subscript(index: Int) -> Int {
        return multiplier * index
    }
}
let threeTimesTable = TimesTable(multiplier: 3)
println("six times three is \(threeTimesTable[6])")
// prints "six times three is 18"
```

```
struct TimesTable {
	let multiplier: Int
	subscript(index: Int) -> Int {
		return multiplier * index
	}
}
let threeTimesTable = TimesTable(multiplier: 3)
println("3的6倍是\(threeTimesTable[6])")
// 输出 "3的6倍是18"
```

In this example, a new instance of TimesTable is created to represent the three-times-table. This is indicated by passing a value of 3 to the structure’s initializer as the value to use for the instance’s multiplier parameter.

在上例中，通过TimesTable结构体创建了一个用来表示索引值三倍的实例。数值3作为结构体构造函数入参表示这个值将成为实例成员multiplier的值。

You can query the threeTimesTable instance by calling its subscript, as shown in the call to threeTimesTable[6]. This requests the sixth entry in the three-times-table, which returns a value of 18, or 3 times 6.

你可以通过下标来来得到结果，比如`threeTimesTable[6]`。这句话访问了threeTimesTable的第六个元素，返回18或者6的3倍。

> NOTE
>
> An n-times-table is based on a fixed mathematical rule. It is not appropriate to set threeTimesTable[someIndex] to a new value, and so the subscript for TimesTable is defined as a read-only subscript.

> <b>提示</b>
> 
> TimesTable例子是基于一个固定的数学公式。它并不适合开放写权限来对`threeTimesTable[someIndex]`进行赋值操作，这也是为什么下标只定义为只读的原因。

## Subscript Usage
## 下标用法

The exact meaning of “subscript” depends on the context in which it is used. Subscripts are typically used as a shortcut for accessing the member elements in a collection, list, or sequence. You are free to implement subscripts in the most appropriate way for your particular class or structure’s functionality.

下标根据使用场景不同也具有不同的含义。通常下标是用来访问集合(collection)，列表(list)或序列(sequence)中元素的快捷方式。你可以为特定的类或结构体中自由的实现下标来提供合适的功能。

For example, Swift’s Dictionary type implements a subscript to set and retrieve the values stored in a Dictionary instance. You can set a value in a dictionary by providing a key of the dictionary’s key type within subscript braces, and assigning a value of the dictionary’s value type to the subscript:

例如，Swift的字典(Dictionary)实现了通过下标来对其实例中存放的值进行存取操作。在字典中设值可以通过给字典提供一个符合字典索引类型的索引值的表达式赋一个与字典存放值类型匹配的值来做到：

```
var numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
numberOfLegs["bird"] = 2
```

```
var numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
numberOfLegs["bird"] = 2
```

The example above defines a variable called numberOfLegs and initializes it with a dictionary literal containing three key-value pairs. The type of the numberOfLegs dictionary is inferred to be Dictionary<String, Int>. After creating the dictionary, this example uses subscript assignment to add a String key of "bird" and an Int value of 2 to the dictionary.

上例定义一个名为numberOfLegs的变量并用一个字典表达式初始化出了包含三对键值的字典实例。numberOfLegs的字典存放值类型推断为`Dictionary<String, Int>`。字典实例创建完成之后通过下标的方式将整型值`2`赋值到字典实例的索引为`bird`的位置中。

For more information about Dictionary subscripting, see [Accessing and Modifying a Dictionary](#).

更多关于字典(Dictionary)下标的信息请参考[字典的访问与修改](#)

> NOTE

> Swift’s Dictionary type implements its key-value subscripting as a subscript that takes and receives an optional type. For the numberOfLegs dictionary above, the key-value subscript takes and returns a value of type Int?, or “optional int”. The Dictionary type uses an optional subscript type to model the fact that not every key will have a value, and to give a way to delete a value for a key by assigning a nil value for that key.

> <b>提示</b>
>
> Swift中Dictionary的下标实现中，在get部分返回值是`Int?`，也就是说不是每个字典的索引都能得到一个整型值，对于没有设过值的索引的访问返回的结果就是`nil`；同样想要从字典实例中删除某个索引下的值也只需要给这个索引赋值为`nil`即可。


## Subscript Options
## 下标选项

Subscripts can take any number of input parameters, and these input parameters can be of any type. Subscripts can also return any type. Subscripts can use variable parameters and variadic parameters, but cannot use in-out parameters or provide default parameter values.

下标允许任意数量的入参索引，并且每个入参类型也没有限制。下标的返回值也可以是任何类型。下标可以使用变量参数和可变参数，但使用in-out参数或给参数设置默认值都是不允许的。

A class or structure can provide as many subscript implementations as it needs, and the appropriate subscript to be used will be inferred based on the types of the value or values that are contained within the subscript braces at the point that the subscript is used. This definition of multiple subscripts is known as subscript overloading.

一个类或结构体可以根据自身需要提供多个下标实现，在定义下标时通过入参个类型进行区分，使用下标时会自动匹配合适的下标实现运行，这就是下标的重载。

While it is most common for a subscript to take a single parameter, you can also define a subscript with multiple parameters if it is appropriate for your type. The following example defines a Matrix structure, which represents a two-dimensional matrix of Double values. The Matrix structure’s subscript takes two integer parameters:

一个下标入参是最常见的情况，但只要有合适的场景也可以定义多个下标入参。如下例定义了一个Matrix结构体，将呈现一个Double类型的二维数组。Matrix结构体的下标需要两个整型参数：

```
struct Matrix {
    let rows: Int, columns: Int
    var grid: Double[]
    init(rows: Int, columns: Int) {
        self.rows = rows
        self.columns = columns
        grid = Array(count: rows * columns, repeatedValue: 0.0)
    }
    func indexIsValidForRow(row: Int, column: Int) -> Bool {
        return row >= 0 && row < rows && column >= 0 && column < columns
    }
    subscript(row: Int, column: Int) -> Double {
        get {
            assert(indexIsValidForRow(row, column: column), "Index out of range")
            return grid[(row * columns) + column]
        }
        set {
            assert(indexIsValidForRow(row, column: column), "Index out of range")
            grid[(row * columns) + column] = newValue
        }
    }
}
```

```
struct Matrix {
	let rows: Int, columns: Int
	var grid: Double[]
	init(rows: Int, columns: Int) {
		self.rows = rows
		self.columns = columns
		grid = Array(count: rows * columns, repeatedValue: 0.0)
	}
	func indexIsValidForRow(row: Int, column: Int) -> Bool {
        return row >= 0 && row < rows && column >= 0 && column < columns
    }
    subscript(row: Int, column: Int) -> Double {
        get {
            assert(indexIsValidForRow(row, column: column), "Index out of range")
            return grid[(row * columns) + column]
        }
        set {
            assert(indexIsValidForRow(row, column: column), "Index out of range")
            grid[(row * columns) + columns] = newValue
        }
	}
}
```

Matrix provides an initializer that takes two parameters called rows and columns, and creates an array that is large enough to store rows * columns values of type Double. Each position in the matrix is given an initial value of 0.0. To achieve this, the array’s size, and an initial cell value of 0.0, are passed to an array initializer that creates and initializes a new array of the correct size. This initializer is described in more detail in [Creating and Initializing an Array](#).

Matrix提供了一个两个入参的构造方法，入参分别是`rows`和`columns`，创建了一个足够容纳rows * columns个数的Double类型数组。为了存储，将数组的大小和数组每个元素初始值0.0，都传入数组的构造方法中来创建一个正确大小的新数组。关于数组的构造方法和析构方法请参考[Creating and Initializing an Array](#)。

You can construct a new Matrix instance by passing an appropriate row and column count to its initializer:

你可以通过传入合适的row和column的数量来构造一个新的Matrix实例：

```
var matrix = Matrix(rows: 2, columns: 2)
```

```
var matrix = Matrix(rows: 2, columns: 2)
```

The preceding example creates a new Matrix instance with two rows and two columns. The grid array for this Matrix instance is effectively a flattened version of the matrix, as read from top left to bottom right:

上例中创建了一个新的两行两列的Matrix实例。在阅读顺序从左上到右下的Matrix实例中的数组实例grid是矩阵二维数组的扁平化存储：

```
// 示意图
grid = [0.0, 0.0, 0.0, 0.0]

		col0 	col1
row0   [0.0, 	0.0,
row1	0.0, 	0.0]
```

Values in the matrix can be set by passing row and column values into the subscript, separated by a comma:

将值赋给带有row和column下标的matrix实例表达式可以完成赋值操作，下标入参使用逗号分割

```
matrix[0, 1] = 1.5
matrix[1, 0] = 3.2
```

These two statements call the subscript’s setter to set a value of 1.5 in the top right position of the matrix (where row is 0 and column is 1), and 3.2 in the bottom left position (where row is 1 and column is 0):

上面两句话分别让matrix的右上值为1.5，坐下值为3.2：

```
[0.0, 1.5,
 3.2, 0.0]
```

The Matrix subscript’s getter and setter both contain an assertion to check that the subscript’s row and column values are valid. To assist with these assertions, Matrix includes a convenience method called indexIsValid, which checks whether the requested row or column is outside the bounds of the matrix:

Matrix下标的getter和setter中同时调用了下标入参的row和column是否有效的判断。为了方便进行断言，Matrix包含了一个名为indexIsValid的成员方法，用来确认入参的row或column值是否会造成数组越界：

```
func indexIsValidForRow(row: Int, column: Int) -> Bool {
    return row >= 0 && row < rows && column >= 0 && column < columns
}
```

An assertion is triggered if you try to access a subscript that is outside of the matrix bounds:

断言在下标越界时触发：

```
let someValue = matrix[2, 2]
// 断言将会触发，因为 [2, 2] 已经超过了matrix的最大长度
```

> 译者：这里有个词Computed Properties 这里统一翻译为实例属性了 微软术语引擎里没有这个词

