###基本运算符

An operator is a special symbol or phrase that you use to check, change, or combine values. For example, the addition operator (+) adds two numbers together (as in let i = 1 + 2). More complex examples include the logical AND operator && (as in if enteredDoorCode && passedRetinaScan) and the increment operator ++i, which is a shortcut to increase the value of i by 1.

运算符（operator）是用来检查，改变或者合并值的一种特殊的符号或者短语。举个例子，加操作符（＋）将2个数字相加(i=1+2).更复杂的如逻辑与运算符`&&`,以及缩写形式的，表达i的值加1的自增运算符`i++`。

Swift supports most standard C operators and improves several capabilities to eliminate common coding errors. The assignment operator (=) does not return a value, to prevent it from being mistakenly used when the equal to operator (==) is intended. Arithmetic operators (+, -, *, /, % and so forth) detect and disallow value overflow, to avoid unexpected results when working with numbers that become larger or smaller than the allowed value range of the type that stores them. You can opt in to value overflow behavior by using Swift’s overflow operators, as described in Overflow Operators.


Swift 支持大部分标准 C 语言运算符，且改进了许多特性来避免常规编码错误。赋值操作符（＝）不再返回一个值，从而避免当应该使用相等运算符（==）的地方，错写成赋值符而导致的错误。算术运算符（＋，－，＊，／，％等）会检测值溢出并且不允许溢出，以此来避免当保存变量时，变量大于或小于其类型所能承载的范围时所导致的异常结果。当然你可以使用 Swift 的溢出运算符来实现溢出。详情参见[溢出运算符](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AdvancedOperators.html#//apple_ref/doc/uid/TP40014097-CH27-XID_37)。

Unlike C, Swift lets you perform remainder (%) calculations on floating-point numbers. Swift also provides two range operators (a..b and a...b) not found in C, as a shortcut for expressing a range of values.

与C语言不同，Swift允许你对浮点数进行求余(%)运算，同时还提供C语言没有的两种区间运算符（a..b 和a...b）,以方便我们表达一定区间内的数值。

This chapter describes the common operators in Swift. Advanced Operators covers Swift’s advanced operators, and describes how to define your own custom operators and implement the standard operators for your own custom types.


本章节只描述了 Swift 中的基本运算符，[高级运算符](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AdvancedOperators.html#//apple_ref/doc/uid/TP40014097-CH27-XID_28)包含了高级运算符相关内容，以及如何自定义运算符与通过扩充标准运算符来生成自定义运算符。

###术语

Operators are unary, binary, or ternary:

Unary operators operate on a single target (such as -a). Unary prefix operators appear immediately before their target (such as !b), and unary postfix operators appear immediately after their target (such as i++).
Binary operators operate on two targets (such as 2 + 3) and are infix because they appear in between their two targets.
Ternary operators operate on three targets. Like C, Swift has only one ternary operator, the ternary conditional operator (a ? b : c).
The values that operators affect are operands. In the expression 1 + 2, the + symbol is a binary operator and its two operands are the values 1 and 2.



运算符包括一元运算符，二元运算符，三元运算符。

* 一元运算符是对单一操作对象的操作（如-a）.一元运算符中，前置运算符出现在操作对象的前面（如!b），后置运算符则出现在操作对象的后面（如i++）.
* 二元运算符是对二个操作对象的操作，位于二个操作对象之间（如2+3）
* 三元运算符就是对三个对象的操作，和C语言一样，Swift 只有一个三元运算符，即三元条件运算符（a ? b : c）。

受运算符影响的值叫操作数，在表达式1 + 2中，加符号`+`是二元运算符，它的两个操作数是两个值1和2。

###赋值运算符

The assignment operator (a = b) initializes or updates the value of a with the value of b:

赋值运算符（a = b）,表示通过b来初始化或更新a的值;

	let b = 10
	var a = 5
	a = b
	// a 现在等于 10	

If the right side of the assignment is a tuple with multiple values, its elements can be decomposed into multiple constants or variables at once:

如果赋值运算符右边是一个多元组，它的元素可以马上被拆分为多个常量或值：

	let (x, y) = (1, 2)
	// 此时 x 等于 1, y 等于 2

Unlike the assignment operator in C and Objective-C, the assignment operator in Swift does not itself return a value. The following statement is not valid:	

与 C 语言和 Objective-C 不同，Swift 的赋值操作符并不返回任何值。所以以下代码是错误的：

	if x = y {
    // 这里是错误的, 因为 x = y 并不返回任何值
	}
	
This feature prevents the assignment operator (=) from being used by accident when the equal to operator (==) is actually intended. By making if x = y invalid, Swift helps you to avoid these kinds of errors in your code.


这个特性使你无法把（==）错写成（=），由于if x = y是错误代码，Swift 从代码层面帮你避免了这些错误的产生。

Arithmetic Operators

Swift supports the four standard arithmetic operators for all number types:

Addition (+)
Subtraction (-)
Multiplication (*)
Division (/)

###算术运算符

Swift 支持所有number类型间的标准四则运算：
* 加法(+)
* 减法(-)
* 乘法(*)
* 除法(/)

	1 + 2       // 等于 3
	5 - 3       // 等于 2
	2 * 3       // 等于 6
	10.0 / 2.5  // 等于 4.0

Unlike the arithmetic operators in C and Objective-C, the Swift arithmetic operators do not allow values to overflow by default. You can opt in to value overflow behavior by using Swift’s overflow operators (such as a &+ b). See Overflow Operators.

The addition operator is also supported for String concatenation:
	
和C、Object-C不同的是,Swift 默认不允许在数值运算中出现溢出情况。但你可以使用 Swift 的溢出运算符来达到有目的的溢出（如a &+ b）。详情参见溢出运算符。

加运算符也可用于String的拼接：

	"hello, " + "world"  // 等于 "hello, world"
	
两个`Character`类型的值或一个`String`类型和一个`Character`类型的值，相加会生成一个新的`String`类型的值：

	let dog: Character = "d"
	let cow: Character = "c"
	let dogCow = dog + cow

	// dogCow 现在是 "dc"

详情参见字符，字符串的拼接。


###求余运算符

The remainder operator (a % b) works out how many multiples of b will fit inside a and returns the value that is left over (known as the remainder).

求余运算（a % b）来计算b的多少倍刚刚好可以容入a，之后返回多出来的那部分（余数）。

>NOTE

>The remainder operator (%) is also known as a modulo operator in other languages. However, its behavior in 
>Swift for negative numbers means that it is, strictly speaking, a remainder rather than a modulo operation.


>注意：
求余运算（%）在其他语言也叫取模运算。然而严格说来，Swift对于该运算符对负数的操作结果，"求余"比"取模"更合适些。

Here’s how the remainder operator works. To calculate 9 % 4, you first work out how many 4s will fit inside 9:

这里展示了求余运算符是怎样计算的。若计算9 % 4，你首先要计算出4的多少倍刚好可以融入9中：

![求余](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/remainderInteger_2x.png)

You can fit two 4s inside 9, and the remainder is 1 (shown in orange).

两个4正好装到9里，余数是1（用橙色标出）

在 Swift 中这么来表达：

	9 % 4    // 等于 1

To determine the answer for a % b, the % operator calculates the following equation and returns remainder as its output:

为了得到a % b的结果，%计算了以下等式，并输出余数作为结果：

a = (b × 倍数) + 余数

where some multiplier is the largest number of multiples of b that will fit inside a.

Inserting 9 and 4 into this equation yields:

当倍数取最大值的时候，就会刚好可以容入a中。

The same method is applied when calculating the remainder for a negative value of a:

把9和4代入等式中，我们得1：

	9 = (4 × 2) + 1

Inserting -9 and 4 into the equation yields:

同样的方法，我来们计算 -9 % 4：

	-9 % 4   // 等于 -1
把-9和4代入等式，-2是取到的最大整数：

	-9 = (4 × -2) + -1
	
余数是-1。

The sign of b is ignored for negative values of b. This means that a % b and a % -b always give the same answer.


在对负数b求余时，b的符号会被忽略。这意味着 a % b 和 a % -b的结果是相同的。


###浮点数求余

Unlike the remainder operator in C and Objective-C, Swift’s remainder operator can also operate on floating-point numbers:

与 C 语言和 Objective-C不同，Swift中可以对浮点数进行求余运算。

	8 % 2.5 // 等于 0.5

In this example, 8 divided by 2.5 equals 3, with a remainder of 0.5, so the remainder operator returns a Double value of 0.5.	
	
这个例子中，8除于2.5等于3余0.5，所以结果是一个Double类型的值0.5。

![浮点数求余](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/remainderFloat_2x.png)

Increment and Decrement Operators

Like C, Swift provides an increment operator (++) and a decrement operator (--) as a shortcut to increase or decrease the value of a numeric variable by 1. You can use these operators with variables of any integer or floating-point type.

###自增和自减运算符
和 C 语言一样，Swift 也提供了对变量本身加1或减1这类运算的缩写：自增（++）和自减（--）的运算符。其操作对象可以是整形和浮点类型的变量。

	var i = 0
	++i      // 现在 i = 1

Each time you call ++i, the value of i is increased by 1. Essentially, ++i is shorthand for saying i = i + 1. Likewise, --i can be used as shorthand for i = i - 1.
	
每调用一次++i，i的值就会加1。实际上，++i是i = i + 1的简写，而--i是i = i - 1的简写。

The ++ and -- symbols can be used as prefix operators or as postfix operators. ++i and i++ are both valid ways to increase the value of i by 1. Similarly, --i and i-- are both valid ways to decrease the value of i by 1.

++和--既是前置又是后置运算。++i，i++，--i和i--都是有效的写法。

Note that these operators modify i and also return a value. If you only want to increment or decrement the value stored in i, you can ignore the returned value. However, if you do use the returned value, it will be different based on whether you used the prefix or postfix version of the operator, according to the following rules:

需要注意的是，这些运算符修改了i后有一个返回值。如果你只想修改i的值，那你就可以忽略这个返回值。但如果你想使用返回值，你需要留意前置和后置操作符的返回值是不同的。

If the operator is written before the variable, it increments the variable before returning its value.
If the operator is written after the variable, it increments the variable after returning its value.

当++前置的时候，先自増再返回。
当++后置的时候，先返回再自增。

	var a = 0
	let b = ++a // a 和 b 现在都是 1
	let c = a++ // a 现在 2, 但 c 是 a 自增前的值 1
	
In the example above, let b = ++a increments a before returning its value. This is why both a and b are equal to to the new value of 1.

However, let c = a++ increments a after returning its value. This means that c gets the old value of 1, and a is then updated to equal 2.

Unless you need the specific behavior of i++, it is recommended that you use ++i and --i in all cases, because they have the typical expected behavior of modifying i and returning the result.



上述例子中，`let b = ++a`首先使a自增1，再返回a的值。所以a和b都是新值1。

而let c = a++，先返回了a的值，然后a才自增1。所以c得到了a的旧值1，而a加1后变成2。

除非你需要使用i++的特性，不然推荐你使用++i和--i，因为先修改后返回这样的行为更符合我们的逻辑。

The sign of a numeric value can be toggled using a prefixed -, known as the unary minus operator:

###一元减号运算符

数值的正负号可以使用前缀-（即一元减号运算符）来切换：

	let three = 3
	let minusThree = -three       // minusThree 等于 -3
	let plusThree = -minusThree   // plusThree 等于 3, 或 "负负3"
	
The unary minus operator (-) is prepended directly before the value it operates on, without any white space.


一元减号运算符（-）写在操作数之前，中间没有空格。

Unary Plus Operator

The unary plus operator (+) simply returns the value it operates on, without any change:

###一元加号操作符

一元加号操作符（+）不做任何改变地返回操作数的值。

	let minusSix = -6
	let alsoMinusSix = +minusSix  // alsoMinusSix 等于 -6
虽然一元+做无用功，但当你在使用一元负号来表达负数时，你可以使用一元正号来表达正数，如此你的代码会具有对称美。

##复合赋值
和C 语言一样，Swift 也提供把其他运算符和赋值运算（=）组合的复合赋值运算符，加赋运算（+=）是其中一个例子：

	var a = 1
	a += 2 // a 现在是 3

表达式a += 2是a = a + 2的简写，一个加赋运算就把加法和赋值两件事完成了。
>注意：
复合赋值运算没有返回值，let b = a += 2这类代码是错误。这不同于上面提到的自增和自减运算符。

在表达式章节里有复合运算符的完整列表。 ‌

##比较运算符
swift支持所有c语言中的比较运算

* 等于（a == b）
* 不等于（a != b）
* 大于（a > b）
* 小于（a < b）
* 大于等于（a >= b）
* 小于等于（a <= b）


NOTE

Swift also provides two identity operators (=== and !==), which you use to test whether two object references both refer to the same object instance. For more information, see Classes and Structures.


>注意：
Swift 也提供身份操作符(`===`和`!==`)来判断两个对象是否是同一个对象实例的引用。更多细节可以参考类与结构体。

Each of the comparison operators returns a Bool value to indicate whether or not the statement is true:

每个比较运算符都返回一个布尔值，用来表示一个表达式是否成立：

	1 == 1   // true, 因为 1 等于 1
	2 != 1   // true, 因为 2 不等于 1
	2 > 1    // true, 因为 2 大于 1
	1 < 2    // true, 因为 1 小于2
	1 >= 1   // true, 因为 1 大于等于 1
	2 <= 1   // false, 因为 2 并不小于等于 1

Comparison operators are often used in conditional statements, such as the if statement:

比较运算多用于条件语句，如if条件：

	let name = "world"
	if name == "world" {
    println("hello, world")
	} else {
    println("I'm sorry \(name), but I don't recognize you")
	}
	// 输出 "hello, world", 因为 `name` 就是等于 "world"

For more on the if statement, see Control Flow.


关于if语句，请参考[控制流](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/ControlFlow.html#//apple_ref/doc/uid/TP40014097-CH9-XID_153)。

Ternary Conditional Operator

The ternary conditional operator is a special operator with three parts, which takes the form question ? answer1 : answer2. It is a shortcut for evaluating one of two expressions based on whether question is true or false. If question is true, it evaluates answer1 and returns its value; otherwise, it evaluates answer2 and returns its value.

The ternary conditional operator is shorthand for the code below:

##三元条件运算符
三元条件运算符的特殊之处，在于它是一个包含三个部分的运算符，它的形式是 问题 ? 答案1 :答案2。它简洁地表达了两个表达式：如果问题成立，返回答案1的结果; 如果不成立，返回答案2的结果。


使用三元条件运算简化了以下代码

	if question: {
  	answer1
	} else {
  	answer2
	}
	
Here’s an example, which calculates the pixel height for a table row. The row height should be 50 pixels taller than the content height if the row has a header, and 20 pixels taller if the row doesn’t have a header:


这里有个计算表格行高的例子。如果有表头，那行高应比内容高度要高出50像素; 如果没有表头，只需高出20像素。

	let contentHeight = 40
	let hasHeader = true
	let rowHeight = contentHeight + (hasHeader ? 50 : 20)
	// rowHeight 现在是 90
	
	let contentHeight = 40
	let hasHeader = true
	var rowHeight = contentHeight
	
The preceding example is shorthand for the code below:

这样写会比下面的代码简洁：

	if hasHeader {
	    rowHeight = rowHeight + 50
	} else {
    	rowHeight = rowHeight + 20
	}
	// rowHeight 现在是 90
	
The first example’s use of the ternary conditional operator means that rowHeight can be set to the correct value on a single line of code. This is more concise than the second example, and removes the need for rowHeight to be a variable, because its value does not need to be modified within an if statement.

The ternary conditional operator provides an efficient shorthand for deciding which of two expressions to consider. Use the ternary conditional operator with care, however. Its conciseness can lead to hard-to-read code if overused. Avoid combining multiple instances of the ternary conditional operator into one compound statement.


第一段代码中使用了三元条件运算符，所以一行代码就能让我们得到正确的值。这比第二段代码简洁得多，无需将rowHeight定义成变量，因为它的值无需在if语句中改变。

三元条件运算符提供高效且便捷的方式来表达二选一的选择。需要注意的是，过度使用三元条件运算符，就会使代码变的难以阅读。我们应避免在一个组合语句中使用多个三元条件运算符。

##区间运算符
Swift 提供了两个方便表达一定区间的值的运算符。

Closed Range Operator

The closed range operator (a...b) defines a range that runs from a to b, and includes the values a and b.

The closed range operator is useful when iterating over a range in which you want all of the values to be used, such as with a for-in loop:

###闭区间运算符
闭区间运算符（a...b）定义一个包含从a到b(包括a和b)的所有值的区间。 ‌ 闭区间运算符在迭代一个区间的所有值时是非常有用的，如在for-in循环中：

	for index in 1...5 {
    	println("\(index) * 5 = \(index * 5)")
	}
	// 1 * 5 = 5
	// 2 * 5 = 10
	// 3 * 5 = 15
	// 4 * 5 = 20
	// 5 * 5 = 25

关于for-in，请参考[控制流](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/ControlFlow.html#//apple_ref/doc/uid/TP40014097-CH9-XID_153)。

Half-Closed Range Operator

The half-closed range operator (a..b) defines a range that runs from a to b, but does not include b. It is said to be half-closed because it contains its first value, but not its final value.

Half-closed ranges are particularly useful when you work with zero-based lists such as arrays, where it is useful to count up to (but not including) the length of the list:

###半闭区间运算符
半闭区间（a..b）定义了一个从a到b但不包括b的区间。 之所以称为半闭区间，是因为该区间包含第一个值而不包含最后的值。

半闭区间的实用性在于，当你使用一个初始元素序号为0的列表(如数组)时，可以非常方便地从0枚举到列表的长度。

	let names = ["Anna", "Alex", "Brian", "Jack"]
	let count = names.count
	for i in 0..count {
    println("第 \(i + 1) 个人叫 \(names[i])")
	}
	// 第 1 个人叫 Anna
	// 第 2 个人叫 Alex
	// 第 3 个人叫 Brian
	// 第 4 个人叫 Jack

Note that the array contains four items, but 0..count only counts as far as 3 (the index of the last item in the array), because it is a half-closed range. For more on arrays, see Arrays.

Logical Operators

Logical operators modify or combine the Boolean logic values true and false. Swift supports the three standard logical operators found in C-based languages:

数组有4个元素，但0..count只数到3(最后一个元素的序号)，因为它是半闭区间。关于数组，请查阅[数组章节]()。

##逻辑运算符
逻辑运算符的操作对象是逻辑布尔值。Swift 支持基于 C 语言的三个标准逻辑运算。

* 逻辑非（!a）
* 逻辑与（a && b）
* 逻辑或（a || b）

Logical NOT Operator

The logical NOT operator (!a) inverts a Boolean value so that true becomes false, and false becomes true.

The logical NOT operator is a prefix operator, and appears immediately before the value it operates on, without any white space. It can be read as “not a”, as seen in the following example:


###逻辑非运算符
逻辑非运算符（!a）对一个布尔值取反，使得true变false，false变true。

它是一个前置运算符，需要出现在操作数之前，之间不需要加空格。可以读作非 a。我们看以下的例子：

	let allowedEntry = false
	if !allowedEntry {
    	println("ACCESS DENIED")
	}
	// 输出 "ACCESS DENIED"

The phrase if !allowedEntry can be read as “if not allowed entry.” The subsequent line is only executed if “not allowed entry” is true; that is, if allowedEntry is false.

As in this example, careful choice of Boolean constant and variable names can help to keep code readable and concise, while avoiding double negatives or confusing logic statements.

	

`if !allowedEntry`语句可以读作 "如果 非 alowed entry。"，下一行代码只有在如果 "非 allow entry" 为`true`，即`allowEntry`为`false`时被执行。
在示例代码中，谨慎地选择布尔常量或变量有助于代码的可读性，并且避免使用双重逻辑非运算，或使用混乱的逻辑语句。

Logical AND Operator

The logical AND operator (a && b) creates logical expressions where both values must be true for the overall expression to also be true.

If either value is false, the overall expression will also be false. In fact, if the first value is false, the second value won’t even be evaluated, because it can’t possibly make the overall expression equate to true. This is known as short-circuit evaluation.

This example considers two Bool values and only allows access if both values are true:

###逻辑与运算符
逻辑与运算符`（a && b）`表达了只有`a`和`b`的值都为`true`时，整个表达式的值才会是`true`。
只要任意一个值为`false`，整个表达式的值就为`false`。事实上，如果第一个值为`false`，那么是不会去计算第二个值的，因为它已经不可能影响整个表达式的结果了。这被称做 "短路计算（short-circuit evaluation）"。
以下例子，只有两个`Bool`值都为`true`值的时候才允许进入：

	let enteredDoorCode = true
	let passedRetinaScan = false
	if enteredDoorCode && passedRetinaScan {
    	println("Welcome!")
	} else {
    	println("ACCESS DENIED")
	}
	// 输出 "ACCESS DENIED"

Logical OR Operator

The logical OR operator (a || b) is an infix operator made from two adjacent pipe characters. You use it to create logical expressions in which only one of the two values has to be true for the overall expression to be true.

Like the Logical AND operator above, the Logical OR operator uses short-circuit evaluation to consider its expressions. If the left side of a Logical OR expression is true, the right side is not evaluated, because it cannot change the outcome of the overall expression.

In the example below, the first Bool value (hasDoorKey) is false, but the second value (knowsOverridePassword) is true. Because one value is true, the overall expression also evaluates to true, and access is allowed:



###逻辑或运算符
逻辑或运算符（a || b）是一个由两个连续的`|`组成的中置运算符。它表示两个逻辑表达式中，其中一个为`true`，整个表达式就为`true`。

同逻辑与运算类似，逻辑或也是"短路计算"的，当左端的表达式为`true`时，将不计算右边的表达式了，因为它不可能改变整个表达式的值了。
以下示例代码中，第一个布尔值（hasDoorKey）为`false`，但第二个值（knowsOverridePassword）为`true`，所以整个表达是`true`，于是允许进入：

	let hasDoorKey = false
	let knowsOverridePassword = true
	if hasDoorKey || knowsOverridePassword {
    	println("Welcome!")
	} else {
   	 println("ACCESS DENIED")
	}
	// 输出 "Welcome!"

###组合逻辑
我们可以组合多个逻辑运算来表达一个复合逻辑：

	if enteredDoorCode && passedRetinaScan || hasDoorKey || 	knowsOverridePassword {
    	println("Welcome!")
	} else {
   		 println("ACCESS DENIED")
	}
	// 输出 "Welcome!"

This example uses multiple && and || operators to create a longer compound expression. However, the && and || operators still operate on only two values, so this is actually three smaller expressions chained together. It can be read as:

If we’ve entered the correct door code and passed the retina scan; or if we have a valid door key; or if we know the emergency override password, then allow access.

Based on the values of enteredDoorCode, passedRetinaScan, and hasDoorKey, the first two mini-expressions are false. However, the emergency override password is known, so the overall compound expression still evaluates to true.

Explicit Parentheses

It is sometimes useful to include parentheses when they are not strictly needed, to make the intention of a complex expression easier to read. In the door access example above, it is useful to add parentheses around the first part of the compound expression to make its intent explicit:	
	
这个例子使用了含多个&&和||运算符的复合逻辑。但无论怎样，&&和||始终只能操作两个值。所以这实际是三个子表达式连续操作的结果。我们来解读一下：

如果我们输入了正确的密码(enteredDoorCode)并通过了视网膜扫描(passedRetinaScan); 或者我们有一把有效的钥匙(hasDoorKey); 又或者我们知道紧急情况下重置的密码(knowsOverridePassword)，我们就能把门打开。

若前两种情况，我们都不满足，所以前两个简单逻辑的结果是`false`，但是我们若知道紧急情况下重置的密码，整个复杂表达式的值还是`true`。

###使用括号来明确优先级
为了一个复杂表达式更容易读懂，在合适的地方使用括号来明确优先级是很有效的，虽然它并非必要。在上个关于门的权限的例子中，我们给第一个部分加个括号，使它看起来逻辑更明确：

	if (enteredDoorCode && passedRetinaScan) || hasDoorKey || 	knowsOverridePassword {
    println("Welcome!")
	} else {
    	println("ACCESS DENIED")
	}	
	// 输出 "Welcome!"

这个括号使得前两个值被看成整个逻辑表达中独立的一个部分。虽然有括号和没括号的输出结果是一样的，但对于读代码的人来说，有括号的代码更清晰。可读性比简洁性更重要，请在可以让你代码变清晰地地方加个括号吧！


