# The Basics
# 基础部分

Swift is a new programming language for iOS and OS X app development. Nonetheless, many parts of Swift will be familiar from your experience of developing in C and Objective-C.
	
Swift是一个用于iOS和OS X平台开发的新的编程语言。尽管如此，Swift在很多地方都会和你以往用C语言和Objective-C开发的经验类似。

Swift provides its own versions of all fundamental C and Objective-C types, including Int for integers; Double and Float for floating-point values; Bool for Boolean values; and String for textual data. Swift also provides powerful versions of the two primary collection types, Array and Dictionary, as described in Collection Types.
	
Swift为所有C和Objective-C的基础类型提供了自己的版本，包括整数值Int，浮点值Double和Float，布尔值Bool，以及文本值String。Swift还提供了两个强大的常见集合类型，数组和字典，见[集合类型](link to 集合类型)。

Like C, Swift uses variables to store and refer to values by an identifying name. Swift also makes extensive use of variables whose values cannot be changed. These are known as constants, and are much more powerful than constants in C. Constants are used throughout Swift to make code safer and clearer in intent when you work with values that do not need to change.
	
和C一样，Swift使用具有唯一名称的变量(variables)来储存和指向特定值。Swift还对那些值不能改变的变量进行了扩展，他们也被称为常量(Constants)，Swift中的常量比C中的常量更加强大。在Swift中当你需要处理一些恒定不变的值的时候，使用常量(Constants)可以让代码更加安全和整洁。

In addition to familiar types, Swift introduces advanced types not found in Objective-C. These include tuples, which enable you to create and pass around groupings of values. Tuples can return multiple values from a function as a single compound value.

除了这些我们熟知的类型以外，Swift还有一些在Objective-C中没有的高级类型，包括：元组（tuples），你可以创建和传递一组数值。元组（tuples）可以在函数中以一个复合值的形式返回多个数值。

Swift also introduces optional types, which handle the absence of a value. Optionals say either “there is a value, and it equals x” or “there isn’t a value at all”. Optionals are similar to using nil with pointers in Objective-C, but they work for any type, not just classes. Optionals are safer and more expressive than nil pointers in Objective-C and are at the heart of many of Swift’s most powerful features.
	
Swift还有可选（Optionals）类型，来处理值缺失的情况。可选类型表示“值是x”或者“没有值”。可选类型类似于在Objective-C的指针中使用nil，但是可选类型可以用在任意类型上，而不只是类。相比于Objective-C中的nil，可选类型（Optionals）更加安全和高效，可选类型也是Swift的众多强大的特性的核心。

Optionals are an example of the fact that Swift is a type safe language. Swift helps you to be clear about the types of values your code can work with. If part of your code expects a String, type safety prevents you from passing it an Int by mistake. This enables you to catch and fix errors as early as possible in the development prObjective Cess.
	
可选类型说明了Swift是一个类型安全的语言。Swift让你清楚的知道你的代码中可用的值的类型。如果你期望这部分代码是字符串（String），类型安全性会阻止你错误的给它赋一个整型（Int）的值。这让你在开发的过程中尽早的发现问题。

# Constants and Variables
# 常量和变量

**Constants and variables associate a name (such as maximumNumberOfLoginAttempts or welcomeMessage) with a value of a particular type (such as the number 10 or the string "Hello"). The value of a constant cannot be changed once it is set, whereas a variable can be set to a different value in the future.

常量和变量对应一个变量名（如maximumNumberOfLoginAttempts或welcomeMessage）以及对应类型的值（如数字10或字符串"Hello"）。常量的值一旦设定旧不能改变，变量的值可以改变。

# Declaring Constants and Variables
# 声明常量和变量

Constants and variables must be declared before they are used. You declare constants with the let keyword and variables with the var keyword. Here’s an example of how constants and variables can be used to track the number of login attempts a user has made:

常量和变量必须在使用前声明。用`let`来声明常量，用`var`来声明变量。下面是一个用常量和变量来记录用户尝试登录次数的例子：

	let maximumNumberOfLoginAttempts = 10
	var currentLoginAttempt = 0

This code can be read as:

这段代码可以解读为：

“Declare a new constant called maximumNumberOfLoginAttempts, and give it a value of 10. Then, declare a new variable called currentLoginAttempt, and give it an initial value of 0.”

声明一个新的常量，叫做“登录尝试次数的最大值”，值为10。声明一个新的变量，叫“当前尝试次数”，初始值设为0。

In this example, the maximum number of allowed login attempts is declared as a constant, because the maximum value never changes. The current login attempt counter is declared as a variable, because this value must be incremented after each failed login attempt.

在这个例子中，登录尝试次数的最大值被声明为常量，因为这个最大值不会改变，当前尝试次数被声明为变量，因为这个值在每次失败的登录尝试之后都要增加。

You can declare multiple constants or multiple variables on a single line, separated by commas:

你可以在同一行内声明多个常量或变量，用逗号分割：

	var x = 0.0, y = 0.0, z = 0.0

> NOTE

> If a stored value in your code is not going to change, always declare it as a constant with the let keyword. Use variables only for storing values that need to be able to change.

> 注意

> 当值不会改变时，永远用`let`声明常量。只在值需要改变的时候用变量。

# Type Annotations
# 类型批注

You can provide a type annotation when you declare a constant or variable, to be clear about the kind of values the constant or variable can store. Write a type annotation by placing a colon after the constant or variable name, followed by a space, followed by the name of the type to use.

在声明常量和变量时，你可以提供一个类型批注，来表明这个常量或变量可以储存的值的类型。类型批注的格式是在常量或变量名后加一个冒号，接着是一个空格，接着是要用的类型的名称。

This example provides a type annotation for a variable called welcomeMessage, to indicate that the variable can store String values:

下面是一个叫`welcomeMessage`的变量的类型批注的例子，来说明这个变量可以储存字符串类型的值：

```
var welcomeMessage: String
```

The colon in the declaration means “…of type…,” so the code above can be read as:

这个表达式中冒号表示：“类型是”，所以这段代码的可以解读为：

“Declare a variable called welcomeMessage that is of type String.”

“声明一个叫welcomeMessage的变量，类型是字符串。”

The phrase “of type String” means “can store any String value.” Think of it as meaning “the type of thing” (or “the kind of thing”) that can be stored.

“类型是”表示“可以储存任意的字符串类型的值”。可以把它想作是“一个事物的类型”它可以储存的。（Think of it as meaning “the type of thing” (or “the kind of thing”) that can be stored. 妈蛋这句真心不会翻啊……）

The welcomeMessage variable can now be set to any string value without error:

变量`welcomeMessage`可以被赋值为任意字符串类型的值，而不会报错：

	welcomeMessage = "Hello"

> NOTE

> It is rare that you need to write type annotations in practice. If you provide an initial value for a constant or variable at the point that it is defined, Swift can almost always infer the type to be used for that constant or variable, as described in Type Safety and Type Inference. In the welcomeMessage example above, no initial value is provided, and so the type of the welcomeMessage variable is specified with a type annotation rather than being inferred from an initial value.

> 注意

> 在实践中你需要写类型批注的很少见。如果你在定义一个常量或变量的时候给了它一个初始值，Swift几乎总是可以推断出这个常量或变量使用的类型，参见类型安全（Type Safety）和类型推断（Type Inference）。在上面这个welcomeMessage的例子里，没有提供初始值，所以welcomeMessage这个变量的类型是通过类型批注的形式来指定，而不是通过初始值推断而来。

# Naming Constants and Variables
# 命名常量和变量

You can use almost any character you like for constant and variable names, including Unicode characters:

你可以使用几乎所有你喜欢的符号来命名常量和变量，包括unicode字符：

```
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

Constant and variable names cannot contain mathematical symbols, arrows, private-use (or invalid) Unicode code points, or line- and box-drawing characters. Nor can they begin with a number, although numbers may be included elsewhere within the name.

常量和变量的命名不能包括数学运算符，箭头， 私有（或无效）的unicode码位， 或者线条（line-），以及制表符（box-drawing）字符。也不能以数字开头，尽管数字可以出现在变量名的其他位置。

Once you’ve declared a constant or variable of a certain type, you can’t redeclare it again with the same name, or change it to store values of a different type. Nor can you change a constant into a variable or a variable into a constant.

一旦你声明了常量或变量的特定类型，你不能用同样的名称重新声明，也不能改变它的储值类型，亦不能把常量改为变量或变量改为常量。

> NOTE

> If you need to give a constant or variable the same name as a reserved Swift keyword, you can do so by surrounding the keyword with back ticks (`) when using it as a name. However, you should avoid using keywords as names unless you have absolutely no choice.

> 注意

> 如果你需要给一个常量或变量一个相同的名字作为swift的关键字，你可以在使用这个名字的时候用重音符（`）把关键字包围起来。然而，除非你没有别的选择，你应该避免使用关键字的方式来命名。

You can change the value of an existing variable to another value of a compatible type. In this example, the value of friendlyWelcome is changed from "Hello!" to "Bonjour!":

你可以改变一个已经存在的变量的值，变成另一个适配类型的值。在下面的例子里，变量`friendlyWelcome`的值从"Hello!"变成了"Bonjour!"：

	var friendlyWelcome = "Hello!"
	friendlyWelcome = "Bonjour!"
	// friendlyWelcome is now "Bonjour!"
	// friendlyWelcome的值现在是"Bonjour!"了。

Unlike a variable, the value of a constant cannot be changed once it is set. Attempting to do so is reported as an error when your code is compiled:

和变量不同，常量的值一旦设定就不能更改。尝试这样做会导致代码编译时报错。

	let languageName = "Swift"
	languageName = "Swift++"
	// this is a compile-time error - languageName cannot be changed

# Printing Constants and Variables
# 输出常量和变量

You can print the current value of a constant or variable with the println function:

你可以用`printIn`函数输出常量和变量的当前值：

```
println(friendlyWelcome)
// prints "Bonjour!"
// 输出 "Bonjour!"
```

println is a global function that prints a value, followed by a line break, to an appropriate output. If you are working in Xcode, for example, println prints its output in Xcode’s “console” pane. (A second function, print, performs the same task without appending a line break to the end of the value to be printed.)

`printIn`是一个输出值的全局函数，为了得到良好的输出结果，输出后会加上一个空行。如果你使用的是Xcode，`printIn`会将结果输出到Xcode的调试信息栏。（另一个函数，`print`，会执行几乎相同的任务，除了不会在输出结果之后加空行以外。）

The println function prints any String value you pass to it:

`printIn`函数会输出任何你赋值的字符串：

```
println("This is a string")
// prints "This is a string"
```

The println function can print more complex logging messages, in a similar manner to Cocoa’s NSLog function. These messages can include the current values of constants and variables.

`printIn`函数可以输出更复杂的记录信息，和Cocoa的NSlog函数类似。这些信息可以包含常量和变量的当前值。

Swift uses string interpolation to include the name of a constant or variable as a placeholder in a longer string, and to prompt Swift to replace it with the current value of that constant or variable. Wrap the name in parentheses and escape it with a backslash before the opening parenthesis:

Swift使用字符串内插(string interpolation)的方式将常量或变量名以占位符的形式加入一个长的字符串中，并且提示Swift用常量或变量的当前值取代替它。将名字包裹在括号中并在前面加上反斜扛来转义。

```
println("The current value of friendlyWelcome is \(friendlyWelcome)")
// prints "The current value of friendlyWelcome is Bonjour!"
// 输出 "The current value of friendlyWelcome is Bonjour!"
```

> NOTE

> All options you can use with string interpolation are described in String Interpolation.

> 注意

> 关于字符串插值的详细参数，参见[字符串插值](link)。

# Comments
# 注释

Use comments to include non-executable text in your code, as a note or reminder to yourself. Comments are ignored by the Swift compiler when your code is compiled.

将代码中不会执行的文本，笔记或者备忘，用注释来表达。注释在编译时会被忽略。

Comments in Swift are very similar to comments in C. Single-line comments begin with two forward-slashes (//):

Swift中的注释和C中的注释十分相似。单行的注释以两个正斜杠 (//)开头：

	// this is a comment
	// 这是一个注释

You can also write multiline comments, which start with a forward-slash followed by an asterisk (/*) and end with an asterisk followed by a forward-slash (*/):

你也可以写多行的注释，用一个正斜杠跟着一个星号开头 (/*) ，用一个星号跟着一个正斜杠结束(*/)：

	/* this is also a comment,
	but written over multiple lines */
	/* 这还是一个注释,
	但是是多行的 */

Unlike multiline comments in C, multiline comments in Swift can be nested inside other multiline comments. You write nested comments by starting a multiline comment block and then starting a second multiline comment within the first block. The second block is then closed, followed by the first block:

和C中的多行注释不同，Swift的多行注释可以嵌套在另一个多行注释内部。你可以这样写嵌套的注释：开始一个多行注释块，在第一块多行注释内部跟着开始第二个多行注释。第二个多行注释块结束，然后第一个多行注释块结束。

	/* this is the start of the first multiline comment
	/* this is the second, nested multiline comment */
	this is the end of the first multiline comment */
	/* 这是第一个多行注释开始
	/* 这是第二个，嵌套的多行注释 */
	这是第一个多行注释的结束 */

Nested multiline comments enable you to comment out large blocks of code quickly and easily, even if the code already contains multiline comments.

嵌套的多行注释让你可以简单快捷的注释一大段代码，即使这块代码之前已经有多行注释块。

# Semicolons
# 分号

Unlike many other languages, Swift does not require you to write a semicolon (;) after each statement in your code, although you can do so if you wish. Semicolons are required, however, if you want to write multiple separate statements on a single line:

和其他很多语言不同，Swift并不要求你在代码的每一个语句之后写一个分号(;)，尽管如果你愿意你可以这么做。然而，如果你想在一行里写多个独立的语句，分号是必要的。

	let cat = "🐱"; println(cat)
	// prints "🐱"

# Integers
# 整数

Integers are whole numbers with no fractional component, such as 42 and -23. Integers are either signed (positive, zero, or negative) or unsigned (positive or zero).

整数就是没有小数部分的完整的数字，如42和-23.整数可以有符号（正数，0，或负数），也可以没有符号（正数或0）。

Swift provides signed and unsigned integers in 8, 16, 32, and 64 bit forms. These integers follow a naming convention similar to C, in that an 8-bit unsigned integer is of type UInt8, and a 32-bit signed integer is of type Int32. Like all types in Swift, these integer types have capitalized names.

Swift提供8，16，32和64进制的带符号和不带符号的整数类型。这些整数遵从和C类似的命名约定，在这个约定中，8进制的无符号整数的类型为`UInt8`，而一个32进制的有符号整数的类型是`Int32`。和Swift的所有类型一样，这些整数的类型是首字母大写的。

# Integer Bounds
# 整数边界

You can access the minimum and maximum values of each integer type with its min and max properties:

你可以通过整数类型的`max`和`min`属性来访问它的最大值和最小值：

	let minValue = UInt8.min  // minValue is equal to 0, and is of type UInt8
	let maxValue = UInt8.max  // maxValue is equal to 255, and is of type UInt8
	let minValue = UInt8.min  // 最小值是 0, 类型是 UInt8
	let maxValue = UInt8.max  // 最大值是 255, 类型是 UInt8

The values of these properties are of the appropriate-sized number type (such as UInt8 in the example above) and can therefore be used in expressions alongside other values of the same type.

这些属性值是相应数字类型的合适范围（比如上面例子里的`UInt8`），因此它们可以在其他拥有相同类型值的表达式中沿用。

# Int
# 整数

In most cases, you don’t need to pick a specific size of integer to use in your code. Swift provides an additional integer type, Int, which has the same size as the current platform’s native word size:

在大多数情况下，你不需要在代码中指定整数的范围。Swift提供了一个专门的整数类型，`Int`，它和当前平台的原生长度范围相同。

On a 32-bit platform, Int is the same size as Int32.

在32位的平台上，`Int`和`Int32`范围相同。

On a 64-bit platform, Int is the same size as Int64.

在64位的平台上，`Int`和`Int64`范围相同。

Unless you need to work with a specific size of integer, always use Int for integer values in your code. This aids code consistency and interoperability. Even on 32-bit platforms, Int can store any value between -2,147,483,648 and 2,147,483,647, and is large enough for many integer ranges.

如果你不需要处理特定的整数范围，请在代码中的整数值使用`Int`类型。这有助于代码的一致性和可复用性。即使在32位的平台上，`Int`类型可以储存从-2,147,483,648到2,147,483,647的整数，大多数情况下这足够用了。

# UInt
# 无符号整数

Swift also provides an unsigned integer type, UInt, which has the same size as the current platform’s native word size:

Swift也提供了无符号整数类型，`UInt`,它和当前平台的原生长度范围相同。

On a 32-bit platform, UInt is the same size as UInt32.

在32位的平台上，`UInt`和`UInt32`范围相同。

On a 64-bit platform, UInt is the same size as UInt64.

在64位的平台上，`UInt`和`UInt64`范围相同。

> NOTE

> Use UInt only when you specifically need an unsigned integer type with the same size as the platform’s native word size. If this is not the case, Int is preferred, even when the values to be stored are known to be non-negative. A consistent use of Int for integer values aids code interoperability, avoids the need to convert between different number types, and matches integer type inference, as described in Type Safety and Type Inference.

> 注意

> 只在你需要特别指定无符号整数与当前平台原生长度范围相同时才使用`UInt`，否则，推荐使用`Int`，即使是你知道不会存储负值的时候。使用一致的`Int`整数类型有助于代码的服用，避免了不同数字类型之间的转换，并且匹配整数的类型推断，详见[类型安全和类型推断](link)。

# Floating-Point Numbers
# 浮点型数字

Floating-point numbers are numbers with a fractional component, such as 3.14159, 0.1, and -273.15.

浮点型数字是指有小数部分的数字，比如3.14159, 0.1 和 -273.15。

Floating-point types can represent a much wider range of values than integer types, and can store numbers that are much larger or smaller than can be stored in an Int. Swift provides two signed floating-point number types:

浮点类型比整数类型范围大很多，它可以储存比整数更大或者更小的数。Swift提供了两种有符号的浮点数类型：

Double represents a 64-bit floating-point number. Use it when floating-point values must be very large or particularly precise.

`Double`代表64位浮点数。当你需要特别大和特别精确的值的时候使用`Double`类型。

Float represents a 32-bit floating-point number. Use it when floating-point values do not require 64-bit precision.

`Float`代表32位浮点数。当不需要像64位那么精确的时候使用`Float`就够了。

> NOTE

> Double has a precision of at least 15 decimal digits, whereas the precision of Float can be as little as 6 decimal digits. The appropriate floating-point type to use depends on the nature and range of values you need to work with in your code.

> 注意

> `Double`有至少15位数字的精确度，而`Float`的精确度最少只有6位数字。根据业务需要的值的范围去选择合适的浮点类型。

# Type Safety and Type Inference
# 类型安全和类型推断

Swift is a type safe language. A type safe language encourages you to be clear about the types of values your code can work with. If part of your code expects a String, you can’t pass it an Int by mistake.

Swift是一个类型安全的语言。一个类型安全的语言鼓励你声明代码中使用的值的类型。如果你期望这部分代码是字符串（String），你就不能错误的给它赋一个整型（Int）的值。

Because Swift is type safe, it performs type checks when compiling your code and flags any mismatched types as errors. This enables you to catch and fix errors as early as possible in the development process.

因为Swift是类型安全的，它会在编译时运行类型检查，并且将所有不匹配的类型标记为错误。这让你可以在开发过程中今早的发现和修复问题。

Type-checking helps you avoid errors when you’re working with different types of values. However, this doesn’t mean that you have to specify the type of every constant and variable that you declare. If you don’t specify the type of value you need, Swift uses type inference to work out the appropriate type. Type inference enables a compiler to deduce the type of a particular expression automatically when it compiles your code, simply by examining the values you provide.

当你处理不同类型的值的时候，类型检查帮助你避免错误。然而，这并不意味着你需要给每一个声明的常量和变量指定特定的类型。如果你没有指定特定的类型，Swift会使用类型推断来推断出合适的类型。当编译代码时，类型推断特性使得编译器可以简单的通过检查你提供的值来自动推断出特定表达式的类型。

Because of type inference, Swift requires far fewer type declarations than languages such as C or Objective-C. Constants and variables are still explicitly typed, but much of the work of specifying their type is done for you.

因为有了类型推断，Swift与类似C和Objective-C的语言相比需要更少的类型声明。常量和变量同样会有准确的类型，但是大部分关于指定类型的工作Swift已经帮你做好了。

Type inference is particularly useful when you declare a constant or variable with an initial value. This is often done by assigning a literal value (or literal) to the constant or variable at the point that you declare it. (A literal value is a value that appears directly in your source code, such as 42 and 3.14159 in the examples below.)

当你声明一个有初始值的常量或变量的时候类型推断特别实用。通常是当你声明一个常量和变量的时候你就给它赋一个参数值（literal value）。（参数值是会直接出现在源码里的值，比如下面例子里的42和3.14159。）

For example, if you assign a literal value of 42 to a new constant without saying what type it is, Swift infers that you want the constant to be an Int, because you have initialized it with a number that looks like an integer:

举个例子，如果你给一个新的常量赋了一个参数值42，但没有说它的类型，Swift会推断你希望这个常量是一个整数类型（Int），因为你用了一个像是整数的数字来初始化：

	let meaningOfLife = 42
	// meaningOfLife is inferred to be of type Int
	// meaningOfLife被推断为整数类型（Int）

Likewise, if you don’t specify a type for a floating-point literal, Swift infers that you want to create a Double:

类似的，如果你没有特别指定一个浮点型的参数，Swift会推断你需要一个Double类型的浮点数：

	let pi = 3.14159
	// pi is inferred to be of type Double
	// pi被推断为Double类型

Swift always chooses Double (rather than Float) when inferring the type of floating-point numbers.

在推断浮点型的数字时，Swift总是会选择Double型而不是Float。

If you combine integer and floating-point literals in an expression, a type of Double will be inferred from the context:

如果你将整数型和浮点型的参数值相加，这种情况下会推断为Double类型：

	let anotherPi = 3 + 0.14159
	// anotherPi is also inferred to be of type Double
	// anotherPi也被推断为Double类型

The literal value of 3 has no explicit type in and of itself, and so an appropriate output type of Double is inferred from the presence of a floating-point literal as part of the addition.

参数值3本身并没有准确的类型，因此是通过相加的元素中有一个浮点型的参数值推断出合适的输出类型为Double.

Numeric Literals

Integer literals can be written as:

A decimal number, with no prefix
A binary number, with a 0b prefix
An octal number, with a 0o prefix
A hexadecimal number, with a 0x prefix
All of these integer literals have a decimal value of 17:

let decimalInteger = 17
let binaryInteger = 0b10001       // 17 in binary notation
let octalInteger = 0o21           // 17 in octal notation
let hexadecimalInteger = 0x11     // 17 in hexadecimal notation
Floating-point literals can be decimal (with no prefix), or hexadecimal (with a 0x prefix). They must always have a number (or hexadecimal number) on both sides of the decimal point. They can also have an optional exponent, indicated by an uppercase or lowercase e for decimal floats, or an uppercase or lowercase p for hexadecimal floats.

For decimal numbers with an exponent of exp, the base number is multiplied by 10exp:

1.25e2 means 1.25 × 102, or 125.0.
1.25e-2 means 1.25 × 10-2, or 0.0125.
For hexadecimal numbers with an exponent of exp, the base number is multiplied by 2exp:

0xFp2 means 15 × 22, or 60.0.
0xFp-2 means 15 × 2-2, or 3.75.
All of these floating-point literals have a decimal value of 12.1875:

let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
Numeric literals can contain extra formatting to make them easier to read. Both integers and floats can be padded with extra zeroes and can contain underscores to help with readability. Neither type of formatting affects the underlying value of the literal:

let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
Numeric Type Conversion

Use the Int type for all general-purpose integer constants and variables in your code, even if they are known to be non-negative. Using the default integer type in everyday situations means that integer constants and variables are immediately interoperable in your code and will match the inferred type for integer literal values.

Use other integer types only when they are are specifically needed for the task at hand, because of explicitly-sized data from an external source, or for performance, memory usage, or other necessary optimization. Using explicitly-sized types in these situations helps to catch any accidental value overflows and implicitly documents the nature of the data being used.

Integer Conversion

The range of numbers that can be stored in an integer constant or variable is different for each numeric type. An Int8 constant or variable can store numbers between -128 and 127, whereas a UInt8 constant or variable can store numbers between 0 and 255. A number that will not fit into a constant or variable of a sized integer type is reported as an error when your code is compiled:

let cannotBeNegative: UInt8 = -1
// UInt8 cannot store negative numbers, and so this will report an error
let tooBig: Int8 = Int8.max + 1
// Int8 cannot store a number larger than its maximum value,
// and so this will also report an error
Because each numeric type can store a different range of values, you must opt in to numeric type conversion on a case-by-case basis. This opt-in approach prevents hidden conversion errors and helps make type conversion intentions explicit in your code.

To convert one specific number type to another, you initialize a new number of the desired type with the existing value. In the example below, the constant twoThousand is of type UInt16, whereas the constant one is of type UInt8. They cannot be added together directly, because they are not of the same type. Instead, this example calls UInt16(one) to create a new UInt16 initialized with the value of one, and uses this value in place of the original:

let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
Because both sides of the addition are now of type UInt16, the addition is allowed. The output constant (twoThousandAndOne) is inferred to be of type UInt16, because it is the sum of two UInt16 values.

SomeType(ofInitialValue) is the default way to call the initializer of a Swift type and pass in an initial value. Behind the scenes, UInt16 has an initializer that accepts a UInt8 value, and so this initializer is used to make a new UInt16 from an existing UInt8. You can’t pass in any type here, however—it has to be a type for which UInt16 provides an initializer. Extending existing types to provide initializers that accept new types (including your own type definitions) is covered in Extensions.

Integer and Floating-Point Conversion

Conversions between integer and floating-point numeric types must be made explicit:

let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi equals 3.14159, and is inferred to be of type Double
Here, the value of the constant three is used to create a new value of type Double, so that both sides of the addition are of the same type. Without this conversion in place, the addition would not be allowed.

The reverse is also true for floating-point to integer conversion, in that an integer type can be initialized with a Double or Float value:

let integerPi = Int(pi)
// integerPi equals 3, and is inferred to be of type Int
Floating-point values are always truncated when used to initialize a new integer value in this way. This means that 4.75 becomes 4, and -3.9 becomes -3.

NOTE

The rules for combining numeric constants and variables are different from the rules for numeric literals. The literal value 3 can be added directly to the literal value 0.14159, because number literals do not have an explicit type in and of themselves. Their type is inferred only at the point that they are evaluated by the compiler.

Type Aliases

Type aliases define an alternative name for an existing type. You define type aliases with the typealias keyword.

Type aliases are useful when you want to refer to an existing type by a name that is contextually more appropriate, such as when working with data of a specific size from an external source:

typealias AudioSample = UInt16
Once you define a type alias, you can use the alias anywhere you might use the original name:

var maxAmplitudeFound = AudioSample.min
// maxAmplitudeFound is now 0
Here, AudioSample is defined as an alias for UInt16. Because it is an alias, the call to AudioSample.min actually calls UInt16.min, which provides an initial value of 0 for the maxAmplitudeFound variable.

Booleans

Swift has a basic Boolean type, called Bool. Boolean values are referred to as logical, because they can only ever be true or false. Swift provides two Boolean constant values, true and false:

let orangesAreOrange = true
let turnipsAreDelicious = false
The types of orangesAreOrange and turnipsAreDelicious have been inferred as Bool from the fact that they were initialized with Boolean literal values. As with Int and Double above, you don’t need to declare constants or variables as Bool if you set them to true or false as soon as you create them. Type inference helps make Swift code more concise and readable when it initializes constants or variables with other values whose type is already known.

Boolean values are particularly useful when you work with conditional statements such as the if statement:

if turnipsAreDelicious {
    println("Mmm, tasty turnips!")
} else {
    println("Eww, turnips are horrible.")
}
// prints "Eww, turnips are horrible."
Conditional statements such as the if statement are covered in more detail in Control Flow.

Swift’s type safety prevents non-Boolean values from being be substituted for Bool. The following example reports a compile-time error:

let i = 1
if i {
    // this example will not compile, and will report an error
}
However, the alternative example below is valid:

let i = 1
if i == 1 {
    // this example will compile successfully
}
The result of the i == 1 comparison is of type Bool, and so this second example passes the type-check. Comparisons like i == 1 are discussed in Basic Operators.

As with other examples of type safety in Swift, this approach avoids accidental errors and ensures that the intention of a particular section of code is always clear.

Tuples

Tuples group multiple values into a single compound value. The values within a tuple can be of any type and do not have to be of the same type as each other.

In this example, (404, "Not Found") is a tuple that describes an HTTP status code. An HTTP status code is a special value returned by a web server whenever you request a web page. A status code of 404 Not Found is returned if you request a webpage that doesn’t exist.

let http404Error = (404, "Not Found")
// http404Error is of type (Int, String), and equals (404, "Not Found")
The (404, "Not Found") tuple groups together an Int and a String to give the HTTP status code two separate values: a number and a human-readable description. It can be described as “a tuple of type (Int, String)”.

You can create tuples from any permutation of types, and they can contain as many different types as you like. There’s nothing stopping you from having a tuple of type (Int, Int, Int), or (String, Bool), or indeed any other permutation you require.

You can decompose a tuple’s contents into separate constants or variables, which you then access as usual:

let (statusCode, statusMessage) = http404Error
println("The status code is \(statusCode)")
// prints "The status code is 404"
println("The status message is \(statusMessage)")
// prints "The status message is Not Found"
If you only need some of the tuple’s values, ignore parts of the tuple with an underscore (_) when you decompose the tuple:

let (justTheStatusCode, _) = http404Error
println("The status code is \(justTheStatusCode)")
// prints "The status code is 404"
Alternatively, access the individual element values in a tuple using index numbers starting at zero:

println("The status code is \(http404Error.0)")
// prints "The status code is 404"
println("The status message is \(http404Error.1)")
// prints "The status message is Not Found"
You can name the individual elements in a tuple when the tuple is defined:

let http200Status = (statusCode: 200, description: "OK")
If you name the elements in a tuple, you can use the element names to access the values of those elements:

println("The status code is \(http200Status.statusCode)")
// prints "The status code is 200"
println("The status message is \(http200Status.description)")
// prints "The status message is OK"
Tuples are particularly useful as the return values of functions. A function that tries to retrieve a web page might return the (Int, String) tuple type to describe the success or failure of the page retrieval. By returning a tuple with two distinct values, each of a different type, the function provides more useful information about its outcome than if it could only return a single value of a single type. For more information, see Functions with Multiple Return Values.

NOTE

Tuples are useful for temporary groups of related values. They are not suited to the creation of complex data structures. If your data structure is likely to persist beyond a temporary scope, model it as a class or structure, rather than as a tuple. For more information, see Classes and Structures.

Optionals

You use optionals in situations where a value may be absent. An optional says:

There is a value, and it equals x
or

There isn’t a value at all
NOTE

The concept of optionals doesn’t exist in C or Objective-C. The nearest thing in Objective-C is the ability to return nil from a method that would otherwise return an object, with nil meaning “the absence of a valid object.” However, this only works for objects—it doesn’t work for structs, basic C types, or enumeration values. For these types, Objective-C methods typically return a special value (such as NSNotFound) to indicate the absence of a value. This approach assumes that the method’s caller knows there is a special value to test against and remembers to check for it. Swift’s optionals let you indicate the absence of a value for any type at all, without the need for special constants.

Here’s an example. Swift’s String type has a method called toInt, which tries to convert a String value into an Int value. However, not every string can be converted into an integer. The string "123" can be converted into the numeric value 123, but the string "hello, world" does not have an obvious numeric value to convert to.

The example below uses the toInt method to try to convert a String into an Int:

let possibleNumber = "123"
let convertedNumber = possibleNumber.toInt()
// convertedNumber is inferred to be of type "Int?", or "optional Int"
Because the toInt method might fail, it returns an optional Int, rather than an Int. An optional Int is written as Int?, not Int. The question mark indicates that the value it contains is optional, meaning that it might contain some Int value, or it might contain no value at all. (It can’t contain anything else, such as a Bool value or a String value. It’s either an Int, or it’s nothing at all.)

If Statements and Forced Unwrapping

You can use an if statement to find out whether an optional contains a value. If an optional does have a value, it evaluates to true; if it has no value at all, it evaluates to false.

Once you’re sure that the optional does contain a value, you can access its underlying value by adding an exclamation mark (!) to the end of the optional’s name. The exclamation mark effectively says, “I know that this optional definitely has a value; please use it.” This is known as forced unwrapping of the optional’s value:

if convertedNumber {
    println("\(possibleNumber) has an integer value of \(convertedNumber!)")
} else {
    println("\(possibleNumber) could not be converted to an integer")
}
// prints "123 has an integer value of 123"
For more on the if statement, see Control Flow.

NOTE

Trying to use ! to access a non-existent optional value triggers a runtime error. Always make sure that an optional contains a non-nil value before using ! to force-unwrap its value.

Optional Binding

You use optional binding to find out whether an optional contains a value, and if so, to make that value available as a temporary constant or variable. Optional binding can be used with if and while statements to check for a value inside an optional, and to extract that value into a constant or variable, as part of a single action. if and while statements are described in more detail in Control Flow.

Write optional bindings for the if statement as follows:

if let constantName = someOptional {
    statements
}
You can rewrite the possibleNumber example from above to use optional binding rather than forced unwrapping:

if let actualNumber = possibleNumber.toInt() {
    println("\(possibleNumber) has an integer value of \(actualNumber)")
} else {
    println("\(possibleNumber) could not be converted to an integer")
}
// prints "123 has an integer value of 123"
This can be read as:

“If the optional Int returned by possibleNumber.toInt contains a value, set a new constant called actualNumber to the value contained in the optional.”

If the conversion is successful, the actualNumber constant becomes available for use within the first branch of the if statement. It has already been initialized with the value contained within the optional, and so there is no need to use the ! suffix to access its value. In this example, actualNumber is simply used to print the result of the conversion.

You can use both constants and variables with optional binding. If you wanted to manipulate the value of actualNumber within the first branch of the if statement, you could write if var actualNumber instead, and the value contained within the optional would be made available as a variable rather than a constant.

nil

You set an optional variable to a valueless state by assigning it the special value nil:

var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
serverResponseCode = nil
// serverResponseCode now contains no value
NOTE

nil cannot be used with non-optional constants and variables. If a constant or variable in your code needs to be able to cope with the absence of a value under certain conditions, always declare it as an optional value of the appropriate type.

If you define an optional constant or variable without providing a default value, the constant or variable is automatically set to nil for you:

var surveyAnswer: String?
// surveyAnswer is automatically set to nil
NOTE

Swift’s nil is not the same as nil in Objective-C. In Objective-C, nil is a pointer to a non-existent object. In Swift, nil is not a pointer—it is the absence of a value of a certain type. Optionals of any type can be set to nil, not just object types.

Implicitly Unwrapped Optionals

As described above, optionals indicate that a constant or variable is allowed to have “no value”. Optionals can be checked with an if statement to see if a value exists, and can be conditionally unwrapped with optional binding to access the optional’s value if it does exist.

Sometimes it is clear from a program’s structure that an optional will always have a value, after that value is first set. In these cases, it is useful to remove the need to check and unwrap the optional’s value every time it is accessed, because it can be safely assumed to have a value all of the time.

These kinds of optionals are defined as implicitly unwrapped optionals. You write an implicitly unwrapped optional by placing an exclamation mark (String!) rather than a question mark (String?) after the type that you want to make optional.

Implicitly unwrapped optionals are useful when an optional’s value is confirmed to exist immediately after the optional is first defined and can definitely be assumed to exist at every point thereafter. The primary use of implicitly unwrapped optionals in Swift is during class initialization, as described in Unowned References and Implicitly Unwrapped Optional Properties.

An implicitly unwrapped optional is a normal optional behind the scenes, but can also be used like a nonoptional value, without the need to unwrap the optional value each time it is accessed. The following example shows the difference in behavior between an optional String and an implicitly unwrapped optional String:

let possibleString: String? = "An optional string."
println(possibleString!) // requires an exclamation mark to access its value
// prints "An optional string."
 
let assumedString: String! = "An implicitly unwrapped optional string."
println(assumedString)  // no exclamation mark is needed to access its value
// prints "An implicitly unwrapped optional string."
You can think of an implicitly unwrapped optional as giving permission for the optional to be unwrapped automatically whenever it is used. Rather than placing an exclamation mark after the optional’s name each time you use it, you place an exclamation mark after the optional’s type when you declare it.

NOTE

If you try to access an implicitly unwrapped optional when it does not contain a value, you will trigger a runtime error. The result is exactly the same as if you place an exclamation mark after a normal optional that does not contain a value.

You can still treat an implicitly unwrapped optional like a normal optional, to check if it contains a value:

if assumedString {
    println(assumedString)
}
// prints "An implicitly unwrapped optional string."
You can also use an implicitly unwrapped optional with optional binding, to check and unwrap its value in a single statement:

if let definiteString = assumedString {
    println(definiteString)
}
// prints "An implicitly unwrapped optional string."
NOTE

Implicitly unwrapped optionals should not be used when there is a possibility of a variable becoming nil at a later point. Always use a normal optional type if you need to check for a nil value during the lifetime of a variable.

Assertions

Optionals enable you to check for values that may or may not exist, and to write code that copes gracefully with the absence of a value. In some cases, however, it is simply not possible for your code to continue execution if a value does not exist, or if a provided value does not satisfy certain conditions. In these situations, you can trigger an assertion in your code to end code execution and to provide an opportunity to debug the cause of the absent or invalid value.

Debugging with Assertions

An assertion is a runtime check that a logical condition definitely evaluates to true. Literally put, an assertion “asserts” that a condition is true. You use an assertion to make sure that an essential condition is satisfied before executing any further code. If the condition evaluates to true, code execution continues as usual; if the condition evaluates to false, code execution ends, and your app is terminated.

If your code triggers an assertion while running in a debug environment, such as when you build and run an app in Xcode, you can see exactly where the invalid state occurred and query the state of your app at the time that the assertion was triggered. An assertion also lets you provide a suitable debug message as to the nature of the assert.

You write an assertion by calling the global assert function. You pass the assert function an expression that evaluates to true or false and a message that should be displayed if the result of the condition is false:

let age = -3
assert(age >= 0, "A person's age cannot be less than zero")
// this causes the assertion to trigger, because age is not >= 0
In this example, code execution will continue only if age >= 0 evaluates to true, that is, if the value of age is non-negative. If the value of age is negative, as in the code above, then age >= 0 evaluates to false, and the assertion is triggered, terminating the application.

Assertion messages cannot use string interpolation. The assertion message can be omitted if desired, as in the following example:

assert(age >= 0)
When to Use Assertions

Use an assertion whenever a condition has the potential to be false, but must definitely be true in order for your code to continue execution. Suitable scenarios for an assertion check include:

An integer subscript index is passed to a custom subscript implementation, but the subscript index value could be too low or too high.
A value is passed to a function, but an invalid value means that the function cannot fulfill its task.
An optional value is currently nil, but a non-nil value is essential for subsequent code to execute successfully.
See also Subscripts and Functions.

NOTE

Assertions cause your app to terminate and are not a substitute for designing your code in such a way that invalid conditions are unlikely to arise. Nonetheless, in situations where invalid conditions are possible, an assertion is an effective way to ensure that such conditions are highlighted and noticed during development, before your app is published.