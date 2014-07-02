# 基础部分

Swift是一个用于iOS和OS X平台开发的新的编程语言。尽管如此，Swift在很多地方都会和你以往用C语言和Objective-C开发的经验类似。

Swift为所有C和Objective-C的基础类型提供了自己的版本，包括整数值`Int`，浮点值`Double`和`Float`，布尔值`Bool`，以及文本值`String`。Swift还提供了两个强大的常见集合类型，数组`Array`和字典`Dictionary`，见[集合类型](link)。

和C一样，Swift使用具有唯一名称的变量（variables）来储存和指向特定值。Swift还对那些值不能改变的变量进行了扩展，他们也被称为常量（Constants），Swift中的常量比C中的常量更加强大。在Swift中当你需要处理一些恒定不变的值的时候，使用常量（Constants）可以让代码更加安全和整洁。

除了这些我们熟知的类型以外，Swift还有一些在Objective-C中没有的高级类型，比如可以创建和传递一组数值的元组（tuples）。元组能在函数中以一个复合值的形式返回多个值。

Swift还有可选（Optionals）类型，来处理值缺失的情况。可选类型表示“值是x”或者“没有值”。可选类型类似于在Objective-C的指针中使用`nil`，但是可选类型可以用在任意类型上，而不只是类。相比于Objective-C中的`nil`，可选类型（Optionals）更加安全和高效，可选类型也是Swift的众多强大<del>的</del>特性的核心。

可选类型说明了Swift是一个类型安全的语言。Swift让你清楚的知道你的代码中可用的值的类型。如果你期望这部分代码是字符串（`String`），类型安全性会阻止你错误的给它赋一个整型（`Int`）的值。这让你在开发的过程中尽早的发现***和解决***问题。

# 常量和变量

常量和变量将一个变量名（如`maximumNumberOfLoginAttempts`或`welcomeMessage`）和对应类型的值（如数字`10`或字符串`"Hello"`）进行关联。常量的值一旦设定就不能改变，变量的值可以。

# 声明常量和变量

常量和变量必须在使用前声明。用`let`来声明常量，用`var`来声明变量。下面是一个用常量和变量来记录用户尝试登录次数的例子：

```
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
```

这段代码可以解读为：

“Declare a new constant called maximumNumberOfLoginAttempts, and give it a value of 10. Then, declare a new variable called currentLoginAttempt, and give it an initial value of 0.”

声明一个新的常量，叫做`maximumNumberOfLoginAttempts`（最大尝试登陆次数），值为`10`。声明一个新的变量，叫做`currentLoginAttempt`（当前尝试登陆次数），初始值设为`0`。

在这个例子中，最大尝试登陆次数被声明为常量，因为这个最大值不会改变，当前尝试登陆次数被声明为变量，因为这个值在每次尝试登陆失败后都要增加。

你可以在同一行内声明多个常量或变量，用逗号分割：

```
var x = 0.0, y = 0.0, z = 0.0
```

> 注意

> 当值不会改变时，永远用`let`声明常量。只在值需要改变的时候用变量。

# 类型批注

在声明常量和变量时，你可以提供一个类型批注，来表明这个常量或变量可以储存的值的类型。类型批注的格式是在常量或变量名后加一个冒号，接着是一个空格，接着是要使用的类型的名称。

下面是一个叫`welcomeMessage`的变量的类型批注的例子，来说明这个变量可以储存`String`（字符串）类型的值：

```
var welcomeMessage: String
```

这个声明中的冒号表示“类型是”，所以这段代码可以解读为：

“声明一个叫`welcomeMessage`的变量，类型是`String`（字符串）。”

“类型是`String`（字符串）”表示“可以储存任意的`String`（字符串）类型的值”。可以把它想作是它可以储存的“一个事物的类型”。

变量`welcomeMessage`可以被赋值为任意`String`（字符串）类型的值，而不会报错：

```
welcomeMessage = "Hello"
```

> 注意

> 在实践中你很少需要写类型批注。如果你在定义一个常量或变量时给了它一个初始值，Swift几乎总是可以推断出这个常量或变量使用的类型，参见[类型安全和类型推断](link)。在上面这个welcomeMessage的例子里，没有提供初始值，所以`welcomeMessage`这个变量的类型通过类型批注的形式指定，而不是从初始值推断而来。

# 命名常量和变量

你可以使用几乎所有你喜欢的符号来命名常量和变量，包括unicode字符：

```
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

常量和变量的命名不能包括数学运算符，箭头， 私有（或无效）的unicode码位， 或者线条（line-），以及制表符（box-drawing）字符。也不能以数字开头，尽管数字可以出现在变量名的其他位置。

一旦你声明了常量或变量为特定类型，你不能用同样的名称重新声明，不能改变它的储值类型，也不能把常量改为变量或变量改为常量。

> NOTE

> If you need to give a constant or variable the same name as a reserved Swift keyword, you can do so by surrounding the keyword with back ticks (`) when using it as a name. However, you should avoid using keywords as names unless you have absolutely no choice.

> 注意

> 如果你需要给一个常量或变量一个相同的名字作为swift的关键字，你可以在使用这个名字的时候用重音符（`）把关键字包围起来。然而，除非你没有别的选择，你应该避免使用关键字的方式来命名。

You can change the value of an existing variable to another value of a compatible type. In this example, the value of friendlyWelcome is changed from "Hello!" to "Bonjour!":

你可以<del>改变一个已经存在的变量的值，变成另一个适配类型的值</del>将一个已经存在的变量的值改变成另一个适配类型的值。在下面的例子里，变量`friendlyWelcome`的值从`"Hello!"`变成了`"Bonjour!"`：

```
var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome is now "Bonjour!"
```

```
var friendlyWelcome = "Hello!"
friendlyWelcome = "Bonjour!"
// friendlyWelcome的值现在是"Bonjour!"了。
```

Unlike a variable, the value of a constant cannot be changed once it is set. Attempting to do so is reported as an error when your code is compiled:

和变量不同，常量的值一旦设定就不能更改。尝试更改会导致代码编译时报错。

```
let languageName = "Swift"
languageName = "Swift++"
// this is a compile-time error - languageName cannot be changed
```

# Printing Constants and Variables
# 输出常量和变量

You can print the current value of a constant or variable with the println function:

你可以用`printIn`函数输出常量和变量的当前值：

```
println(friendlyWelcome)
// prints "Bonjour!"
```

```
println(friendlyWelcome)
// 输出 "Bonjour!"
```

println is a global function that prints a value, followed by a line break, to an appropriate output. If you are working in Xcode, for example, println prints its output in Xcode’s “console” pane. (A second function, print, performs the same task without appending a line break to the end of the value to be printed.)

`printIn`是一个输出值的全局函数，为了得到良好的输出结果，输出后会加上一个空行。如果你使用的是Xcode，`printIn`会将结果输出到Xcode的调试信息栏。（另一个函数，`print`，会执行几乎相同的任务，除了不会在输出结果之后加空行以外。）

The println function prints any String value you pass to it:

`printIn`函数会输出任何你<del>赋值的字符串</del>传递给它的字符串（`String`）值：

```
println("This is a string")
// prints "This is a string"
```

The println function can print more complex logging messages, in a similar manner to Cocoa’s NSLog function. These messages can include the current values of constants and variables.

`printIn`函数可以输出更复杂的记录信息，和Cocoa的`NSlog`函数类似。这些信息可以包含常量和变量的当前值。

Swift uses string interpolation to include the name of a constant or variable as a placeholder in a longer string, and to prompt Swift to replace it with the current value of that constant or variable. Wrap the name in parentheses and escape it with a backslash before the opening parenthesis:

Swift使用字符串<del>内插</del>插值（string interpolation）的方式将常量或变量名以占位符的形式加入<del>一个长的</del>字符串中，并且提示Swift用常量或变量的当前值<del>取代替它</del>替换对应占位符。书写格式是将名字包裹在括号中并在前面加上反斜扛来转义：

```
println("The current value of friendlyWelcome is \(friendlyWelcome)")
// prints "The current value of friendlyWelcome is Bonjour!"
```
```
println("The current value of friendlyWelcome is \(friendlyWelcome)")
// 输出 "The current value of friendlyWelcome is Bonjour!"
```

> NOTE

> All options you can use with string interpolation are described in String Interpolation.

> 注意

> 关于字符串插值的详细参数，参见[字符串插值](link)。

# Comments
# 注释

Use comments to include non-executable text in your code, as a note or reminder to yourself. Comments are ignored by the Swift compiler when your code is compiled.

将代码中不会执行的文本，笔记或者备忘用注释来表达。注释在代码编译时会被忽略。

Swift中的注释和C中的注释十分相似。单行的注释以两个正斜杠（```//```）开头：

```
// 这是一个注释
```

你也可以写多行的注释，用一个正斜杠跟着一个星号开头（`/*`），用一个星号跟着一个正斜杠结束（`*/`）：

```
/* 这还是一个注释,
但是是多行的 */
```

和C中的多行注释不同，Swift的多行注释可以嵌套在另一个多行注释内部。你可以这样写嵌套的注释：开始一个多行注释块，在第一块多行注释内部跟着开始第二个多行注释。第二个多行注释块结束，然后第一个多行注释块结束。

```
/* 这是第一个多行注释开始
/* 这是第二个，嵌套的多行注释 */
这是第一个多行注释的结束 */
```

嵌套的多行注释让你可以简单快捷的注释一大段代码，即使这段代码之前已经有多行注释块。

# 分号

和其他很多语言不同，Swift并不要求你在代码的每一个语句之后写一个分号（`;`），尽管如果你愿意你可以这么做。然而，如果你想在一行里写多个独立的语句，分号是必要的。

	let cat = "🐱"; println(cat)
	// prints "🐱"

# 整数

整数就是没有小数部分的完整数字，如`42`和`-23`。整数可以有符号（正数，0，或负数），也可以没有符号（正数或0）。

Swift提供8，16，32和64位的带符号和不带符号的整数类型。这些整数遵从和C类似的命名约定，在这个约定中，8位的无符号整数的类型为`UInt8`，而32位的有符号整数的类型是`Int32`。和Swift的所有类型一样，这些整数的类型是首字母大写的。

## 整数边界

你可以通过整数类型的`max`和`min`属性来访问它的最大值和最小值：

```
let minValue = UInt8.min  // 最小值是 0, 类型是 UInt8
let maxValue = UInt8.max  // 最大值是 255, 类型是 UInt8
```

这些属性值是相应数字类型的合适范围（比如上面例子里的`UInt8`），因此它们可以在其他拥有相同类型值的表达式中沿用。

## 整数

在大多数情况下，你不需要在代码中指定整数的范围。Swift提供了一个专门的整数类型`Int`，它和当前平台的原生长度范围相同。

* 在32位的平台上，`Int`和`Int32`范围相同。
* 在64位的平台上，`Int`和`Int64`范围相同。

如果你不需要处理特定的整数范围，请在代码中始终使用`Int`类型。这有助于代码的一致性和可复用性。即使在32位的平台上，`Int`类型可以储存从`-2,147,483,648`到`2,147,483,647`的整数，大多数情况下这足够用了。

## 无符号整数

Swift也提供了无符号整数类型，`UInt`，它和当前平台的原生长度范围相同。

* 在32位的平台上，`UInt`和`UInt32`范围相同。
* 在64位的平台上，`UInt`和`UInt64`范围相同。

> NOTE

> Use UInt only when you specifically need an unsigned integer type with the same size as the platform’s native word size. If this is not the case, Int is preferred, even when the values to be stored are known to be non-negative. A consistent use of Int for integer values aids code interoperability, avoids the need to convert between different number types, and matches integer type inference, as described in Type Safety and Type Inference.

> 注意

> 只在你需要特别指定无符号整数与当前平台原生长度范围相同时才使用`UInt`，否则，推荐使用`Int`，即使是你知道不会存储负值的时候。使用一致的`Int`整数类型有助于代码的复用，避免了不同数字类型之间的转换，并且和整数的类型推断结果一致，详见[类型安全和类型推断](link)。

# 浮点型数字

浮点型数字是指有小数部分的数字，比如`3.14159`，`0.1`和`-273.15`。

浮点类型比整数类型范围大很多，它可以储存比整数更大或者更小的数。Swift提供了两种有符号的浮点数类型：

* Double represents a 64-bit floating-point number. Use it when floating-point values must be very large or particularly precise.
* Float represents a 32-bit floating-point number. Use it when floating-point values do not require 64-bit precision.

* `Double`代表64位浮点数。当你需要特别大和特别精确的值的时候使用`Double`类型。
* `Float`代表32位浮点数。当不需要像64位那么精确的时候使用`Float`就够了。

> NOTE

> Double has a precision of at least 15 decimal digits, whereas the precision of Float can be as little as 6 decimal digits. The appropriate floating-point type to use depends on the nature and range of values you need to work with in your code.

> 注意

> `Double`有至少15位数字的精确度，而`Float`的精确度只有至少6位数字。根据业务需要的值的范围去选择合适的浮点类型。

# 类型安全和类型推断

Swift是一个类型安全的语言。一个类型安全的语言鼓励你声明代码中使用的值的类型。如果你期望这部分代码是`String`（字符串），你就不能错误的给它赋一个`Int`（整型）的值。

因为Swift是类型安全的，它会在代码编译时运行类型检查，并且将所有不匹配的类型标记为错误。这让你可以在开发过程中今早的发现和修复问题。

当你处理不同类型的值的时候，类型检查帮助你避免错误。然而，这并不意味着你需要给每一个声明的常量和变量指定特定的类型。如果你没有指定特定的类型，Swift会使用类型推断来推断出合适的类型。当编译代码时，类型推断特性使得编译器可以简单的通过检查你提供的值来自动推断出特定表达式的类型。

因为有了类型推断，Swift与类似C和Objective-C的语言相比需要更少的类型声明。常量和变量同样会有准确的类型，但是大部分关于指定类型的工作Swift已经帮你做好了。

当你声明一个有初始值的常量或变量时类型推断特别实用。通常是当你声明一个常量和变量的时候你就给它赋一个字面量（literal value）。（字面量是会直接出现在源码里的值，比如下面例子里的`42`和`3.14159`。）

举个例子，如果你给一个新的常量赋了一个字面量`42`，但没有指定它的类型，Swift会推断你希望这个常量是一个`Int`（整数）类型，因为你用了一个像是整数的数字来初始化变量：

```
let meaningOfLife = 42
// meaningOfLife被推断为Int（整数）类型
```

类似的，如果你没有特别指定一个浮点型的字面量，Swift会推断你需要一个`Double`类型的浮点数：

```
let pi = 3.14159
// pi被推断为Double类型
```

在推断浮点型的数字时，Swift总是会选择`Double`类型而不是`Float`类型。

如果你将整数型和浮点型的字面量相加，这种情况下会推断为`Double`类型：

```
let anotherPi = 3 + 0.14159
// anotherPi也被推断为Double类型
```

字面量`3`本身并没有准确的类型，因此是通过相加的元素中有一个浮点型的字面量推断出合适的输出类型为`Double`。

# 数字字面量

整数字面量可以写成：

* 十进制的数字，不需要任何前缀
* 二进制的数字，前缀是`0b`
* 八进制的数字，前缀是`0o`
* 十六进制的数字，前缀是`0x`

下面所有的整数字面量在十进制下的值都是`17`：

```
let decimalInteger = 17
let binaryInteger = 0b10001       // 二进制声明中的17
let octalInteger = 0o21           // 八进制声明中的17
let hexadecimalInteger = 0x11     // 十六进制声明中的17
```

浮点型的字面量可以是十进制的（没有前缀），或者十六进制（前缀是`0x`）。在小数点两边都必须有数字（或十六进制数字符号）。它们也可以有一个可选的指数，在十进制中用大写或小写的`e`来表示，在十六进制中用大写或小写的`p`来表示。

在十进制数字中的指数`exp`表示基数乘以10<sup>exp</sup>:

* ```1.25e2``` 表示 1.25 × 10<sup>2</sup>，或者`125.0`.
* ```1.25e-2``` 表示 1.25 × 10<sup>-2</sup>，或者`0.0125`

在十六进制的数字中的指数`exp`表示基数乘以2<sup>exp</sup>

* 0xFp2 表示 15 × 22，或者 60.0.
* 0xFp-2 表示 15 × 2<sup>-2</sup>，或者 3.75.

以下这些浮点字面量在十进制下的值都是`12.1875`：

```
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
```

数字字面量可以使用额外的格式让它们更易读。不论整数还是浮点数都可以添加额外的0，和下划线来增加可读性。这些格式都不会影响到这些字面量原本的值：

```
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
```

# 数字类型转换

在一般情况下对整数的常量或变量使用`Int`类型，即使是你知道不会存储负值的时候。总是使用默认的`Int`（整数）类型意味着你的代码中整数的常量和变量可以很好的协作，并且和整数字面量推断出的类型一致。

只在当前工作中有特殊需要的时候，才使用其他的整数类型，比如是从外部来源的需要指定精确度的数据，或者为了性能，内存使用量，或者其他必要的优化。在这些情况下使用指定精确度的数字类型可以帮助我们发现溢出值和暗示这个数据的特性。

## 整数类型转换

不同整数类型的常量或变量可以储存不同范围的数字。一个`Int8`的常量或变量可以储存`-128`到`127`之间的数字，然而一个`UInt8`型的常量或变量可以储存从`0`到`255`之间的数字。如果一个数字不符合常量或变量的储值范围，编译的时候会报错：

```
let cannotBeNegative: UInt8 = -1
// UInt8不能储存负数，所以这里会报错
let tooBig: Int8 = Int8.max + 1
// Int8不能储存一个大于其最大值的数字
// 所以这里同样会报错
```

因为每一种数字类型可以储存不同范围的值，你必须根据具体的案例选择合适的数字类型转换。这种方式阻止了隐式的转换报错，并且让代码中的类型转换意图更明确。

要将一种特定类型转换成另一种，你需要用一个你想要的类型的新数字值来重新初始化。在下面的例子里，常量`twoThousand`是`UInt16`类型的，然而常量`one`是`UInt8`类型的。它们不能直接相加，因为它们类型不同。因此，这个例子调用了`UInt16(one)`来对常量`one`创建一个新的`UInt16`类型的初始值，然后用这个值来代替原来的值：

```
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
```

因为相加的两个数现在都是`UInt16`类型了，这样相加是允许的。输出结果的常量`twoThousandAndOne`被推断为`UInt16`类型，因为它是两个`UInt16`类型的值的和。

`SomeType(ofInitialValue)`是Swift初始化并赋予一个初值的默认方法。在语言内部，`UInt16`类型有一个初始值设定项会接受一个`UInt8`的值，然后这个初始值设定项是用来从已知的`UInt8`中创建一个新的`UInt16`的值。你不能传递任意类型，只能传入`UInt16`提供初始化的类型。扩展已有的类型来提供更多的初始化选项，来接受新的类型（包括自定义类型），见[扩展](link)。

## 整数和浮点数转换

整数和浮点数之间的类型转换必须是显性的：

```
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi等于3.14159，它被推断为Double类型
```
在这里，常量`three`的值被用来创建一个新的`Double`型的值，所以相加的两个数都是同样的类型了，无须转换，这个加法是允许的。

相对的，由浮点数到整数的转换也是可行的，也就是说一个整数类型可以被初始化为一个`Double`或者`Float`型的值：

```
let integerPi = Int(pi)
// integerPi等于3，它被推断为整数（Int）类型
```

当浮点型的值初始化为一个新的整数型的值时，它的数值总是被截断的。这意味着`4.75`会成为`4`，而`-3.9`会成为`-3`。

> 注意

> 数字的常量和变量相加的规则和数字字面量的规则是不一样的。字面量`3`可以和字面量`0.14159`直接相加，因为数字字面量本身并没有一个显式的类型声明。他们的类型是在编译器运行时被推断的。

# 类型别名

类型别名给已经存在的类型定义另一个名字。你用关键字`typealias`来定义类型别名。

当你想用一个更合适的名字来命名一个已有类型的时候，类型别名是很有用的。比如当你处理需要指定精确度的外部来源数据时：

```
typealias AudioSample = UInt16
```

一旦你定义了类型别名，你就可以在任何你可以使用原始名字的地方使用这个别名：

```
var maxAmplitudeFound = AudioSample.min
// maxAmplitudeFound的值是0
```

Here, AudioSample is defined as an alias for UInt16. Because it is an alias, the call to AudioSample.min actually calls UInt16.min, which provides an initial value of 0 for the maxAmplitudeFound variable.

在这个例子中，`AudioSample`被定义为`UInt16`的一个别名。因为这是一个别名，调用`AudioSample.min`实际上是调用`UInt16.min`给变量`maxAmplitudeFound`赋了初始值`0`。

# 布尔值

Swift有一个基本的布尔值类型，叫做`Bool`。布尔值可以用作逻辑判断，因为它们只有“真”和“假”两个值。Swift提供两种布尔值常量，`true`和`false`：

```
let orangesAreOrange = true
let turnipsAreDelicious = false
```

因为`orangesAreOrange`和`turnipsAreDelicious`有一个布尔的字面量作为初始值，它们的类型被推断为`Bool`。如果你在创建常量或变量的时候就把它们的值设为`true`或者`false`，你不需要声明它们的类型是`Bool`。当你赋予常量或变量一个类型已知的初值时，类型推断让Swift的代码更加准确和可读。

布尔值在条件声明（比如：`if`语句）中特别有用：

```
if turnipsAreDelicious {
    println("Mmm, tasty turnips!")
} else {
    println("Eww, turnips are horrible.")
}
// 输出 "Eww, turnips are horrible."
```

关于条件声明（比如`if`语句）的更多细节会在[Control Flow](link)这一章节中详细讲解。

Swift的类型安全会阻止一个非布尔值替换`Bool`值。下面的例子会在编译时报错：

```
let i = 1
if i {
    // 这个例子不会顺利编译，会报错
}
```

然而，下面这个例子是有效的：

```
let i = 1
if i == 1 {
    // 这个例子会成功编译
}
```

The result of the i == 1 comparison is of type Bool, and so this second example passes the type-check. Comparisons like i == 1 are discussed in Basic Operators.

`i == 1`的比较结果是一个`Bool`类型的值，因此第二个例子通过了类型检查。类似`i == 1`的比较我们会在[Basic Operators](link)进行深入讨论。

和其他Swift的类型安全的例子一样，这种检查避免了意外的错误并且保证了特定的某块代码的意图始终是明确的。

# 元组

元组将多个数值组合成一个单独的复合值。一个元组中的值可以是任何类型，不必是同一种类型。

In this example, (404, "Not Found") is a tuple that describes an HTTP status code. An HTTP status code is a special value returned by a web server whenever you request a web page. A status code of 404 Not Found is returned if you request a webpage that doesn’t exist.

在这个例子里， `(404, "Not Found")` 是一个用来形容HTTP状态码的元组。HTTP状态码是当你请求一个网页的时候网页服务器的返回值。当你请求的网页不存在的时候会返回`404 Not Found`的状态码。

```
let http404Error = (404, "Not Found")
// http404Error的类型是(Int, String)，值等于(404, "Not Found")
```

元组`(404, "Not Found")`将一个整数值`Int`和一个字符串`String`组合起来，给HTTP状态码赋予两个独立的值：一个机器语言的数字和一句人类语言的描述。它可以描述为”一个类型为 `(Int, String)`的元组“。

你可以创建一个含任意类型组合的元组，它们可以包含任意多的类型。谁也不能阻止你创建一个`(Int, Int, Int)`类型或者`(String, Bool)`类型，又或者任意你想要的类型组合的元组。

你可以把一个元组的内容分解成独立的常量或变量，然后你就可以像平常一样引用它们：

```
let (statusCode, statusMessage) = http404Error
println("状态码是 \(statusCode)")
// 输出”状态码是404“
println("状态信息是 \(statusMessage)")
// prints "状态信息是 Not Found"
```
当你在分解元组时，如果只需要元祖的一部分值，可以使用下划线（`_`）来忽略元组的一部分值：

```
let (justTheStatusCode, _) = http404Error
println("The status code is \(justTheStatusCode)")
// prints "The status code is 404"
```

同样的，使用从`0`开始的序列可以引用元组中的一个单独元素的值。

```
println("The status code is \(http404Error.0)")
// prints "The status code is 404"
println("The status message is \(http404Error.1)")
// prints "The status message is Not Found"
```

定义元组的时候，你可以给元素单独命名：

```
let http200Status = (statusCode: 200, description: "OK")
```

如果你给元组中的元素命名了，你可以用这个名字来引用它们的值：

```
println("The status code is \(http200Status.statusCode)")
// prints "The status code is 200"
println("The status message is \(http200Status.description)")
// prints "The status message is OK"
```

Tuples are particularly useful as the return values of functions. A function that tries to retrieve a web page might return the (Int, String) tuple type to describe the success or failure of the page retrieval. By returning a tuple with two distinct values, each of a different type, the function provides more useful information about its outcome than if it could only return a single value of a single type. For more information, see Functions with Multiple Return Values.

作为函数的返回值元组是很有用的。一个试图获取网页的函数可能返回一个(Int, String)类型的元组来描述这个页面获取成功或失败的状态。通过返回一个含有两个不同类型值的元组，这个函数的结果相比只能返回一个单独类型值的函数提供了更多有用的信息。详见[Functions with Multiple Return Values]()。

> 注意

> 当你处理一些相关数据的临时组合，元组是很有用的。它们不适合用于一些复杂的数据类型的创建。如果你的数据结构超过了一个临时的范畴，用class或者structrue会比用元组tuple更合适。更多信息，参见[Classes and Structures](link)。

＃ Optionals
# 可选类型

You use optionals in situations where a value may be absent. An optional says:

当值可能缺失的情况下，可以用可选类型（Options）。可选类型表示：

- There is a value, and it equals x

or

- There isn’t a value at all


- 那里有一个值，它等于x

或者

- 值不存在

> NOTE

> The concept of optionals doesn’t exist in C or Objective-C. The nearest thing in Objective-C is the ability to return nil from a method that would otherwise return an object, with nil meaning “the absence of a valid object.” However, this only works for objects—it doesn’t work for structs, basic C types, or enumeration values. For these types, Objective-C methods typically return a special value (such as NSNotFound) to indicate the absence of a value. This approach assumes that the method’s caller knows there is a special value to test against and remembers to check for it. Swift’s optionals let you indicate the absence of a value for any type at all, without the need for special constants.

> 注意

> 可选类型在C或者Objective-C中都不存在。在Objective-C中最接近的是<del>一个</del>返回一个对象的方法也可以返回一个`nil`值的能力，`nil`的意思是“有效对象的缺失”。然而，它只对对象有效，对`structs`，<del>basic C types, or enumeration values</del>*基本的C类型、或者枚举类型*都是无效的。对这些类型，Objective-C通常会返回一个特殊值（比如`NSNotFound`）来表示值缺失。这样的方式假定我们调用方法时它必须知道有一个特殊值，并且要记得去检查它。Siwft的可选类型让你可以给任意类型的值声明这个值缺失，不需要任何其它的特殊常量。

Here’s an example. Swift’s String type has a method called toInt, which tries to convert a String value into an Int value. However, not every string can be converted into an integer. The string "123" can be converted into the numeric value 123, but the string "hello, world" does not have an obvious numeric value to convert to.

下面是一个例子。Siwft的字符串类型有一个`toInt`的方法，它会尝试将一个字符串类型转换成一个整数类型。然而，不是每一<del>额</del>个字符串都可以转换成整数<del>的</del>。字符串<del>“123”</del>`"123"`可以转换为数字量`123`，但是字符串`"Hello, world"`并没有一个明显的数字量可以转换。

The example below uses the toInt method to try to convert a String into an Int:

下面这个例子用`toInt`方法尝试转换字符串到整数：

```
let possibleNumber = "123"
let convertedNumber = possibleNumber.toInt()
// convertedNumber is inferred to be of type "Int?", or "optional Int"
```

Because the toInt method might fail, it returns an optional Int, rather than an Int. An optional Int is written as Int?, not Int. The question mark indicates that the value it contains is optional, meaning that it might contain some Int value, or it might contain no value at all. (It can’t contain anything else, such as a Bool value or a String value. It’s either an Int, or it’s nothing at all.)

因为`toInt`方法可能失败，它返回的是<del>可以</del>可选类型的整数，而不是一个整数。一个可选的整数表示为`Int?`，而不是`Int`。最后的问号表示这个值是可选的，意味着它可能包含整数类型的值，或者<del>它</del>没有值。（它不能包括其它任何值，比如布尔值或者字符串。它要<del>不</del>么是一个整数，要<del>不</del>么就没有值。）

## If Statements and Forced Unwrapping
## If语句和强制解析

You can use an if statement to find out whether an optional contains a value. If an optional does have a value, it evaluates to true; if it has no value at all, it evaluates to false.

你可以使用`if`语句来判断一个可选类型是否有值。如果有值，它就等于`true`，如果没有值，就等于`false`。

Once you’re sure that the optional does contain a value, you can access its underlying value by adding an exclamation mark (!) to the end of the optional’s name. The exclamation mark effectively says, “I know that this optional definitely has a value; please use it.” This is known as forced unwrapping of the optional’s value:

一旦你确定可选类型是有值的，你可以在可选类型的名字后面加一个感叹号<del>(!)</del>`!`来调用它的值。这个感叹号的意思是：”我知道这个可选类型的值<del>一定</del>存在<del>一个</del>值，请使用这个值。“这叫做可选值的强制解析：

```
if convertedNumber {
    println("\(possibleNumber) has an integer value of \(convertedNumber!)")
} else {
    println("\(possibleNumber) could not be converted to an integer")
}
// prints "123 has an integer value of 123"
```

For more on the if statement, see Control Flow.

更多*`if`语句的*信息，见[Control Flow](link)。

> NOTE

> Trying to use ! to access a non-existent optional value triggers a runtime error. Always make sure that an optional contains a non-nil value before using ! to force-unwrap its value.

> 注意

> 如果你使用`!`来调用一个不存在的可选值，会报<del>出实时</del>运行时错误。在使用`!`强制解析可选值之前<del>总是</del>请确认这个可选值包含一个非`nil`的值。

## Optional Binding
## 可选值绑定

You use optional binding to find out whether an optional contains a value, and if so, to make that value available as a temporary constant or variable. Optional binding can be used with if and while statements to check for a value inside an optional, and to extract that value into a constant or variable, as part of a single action. if and while statements are described in more detail in Control Flow.

你可以使用可选值绑定(optional binding)来找出一个可选类型是否包含值，如果包含，则可以把这个值作为一个临时常量或变量来使用。可选值绑定可以和`if`或`while`语句一起来检查可选值里面的值，并且解析到一个常量或变量中，所有这些都在一步操作中完成。更多关于`if`和`while`语句的信息，见[Control Flow](link)。

Write optional bindings for the if statement as follows:

像这样给`if`语句写可选值绑定：

```
if let constantName = someOptional {
    statements
}
```

You can rewrite the possibleNumber example from above to use optional binding rather than forced unwrapping:

你可以用可选值绑定来代替强制解析来重写之前那个`possibleNumber`的例子：

```
if let actualNumber = possibleNumber.toInt() {
    println("\(possibleNumber) has an integer value of \(actualNumber)")
} else {
    println("\(possibleNumber) could not be converted to an integer")
}
// prints "123 has an integer value of 123"
```

This can be read as:

这段代码可以解读为：

“If the optional Int returned by possibleNumber.toInt contains a value, set a new constant called actualNumber to the value contained in the optional.”

”如果可选整数值通过`possibleNumber.toInt`返回一个值，设定一个叫`actualNumber`的新<del>的</del>常量来储存这个可选整数中的值。“

If the conversion is successful, the actualNumber constant becomes available for use within the first branch of the if statement. It has already been initialized with the value contained within the optional, and so there is no need to use the ! suffix to access its value. In this example, actualNumber is simply used to print the result of the conversion.

如果这个转换是成功的，那么常量`actualNumber`在`if`语句的第一个分支就可用了。它已经用可选量中的值初始化了，所以现在不需要用`!`后缀来调用这个值。在这个例子中，`actualNumber`只是简单的用于输出转换结果。

You can use both constants and variables with optional binding. If you wanted to manipulate the value of actualNumber within the first branch of the if statement, you could write if var actualNumber instead, and the value contained within the optional would be made available as a variable rather than a constant.

无论是常量还是变量你都可以使用可选值绑定。如果你希望对`if`语句第一个分支中`actualNumber`的值进行操作，你可以用`if var actualNumber`来声明，然后可选量中的值就会成为一个可用的变量而不是常量。

## nil
## nil

You set an optional variable to a valueless state by assigning it the special value nil:

<del>给可选变量一个没有值的状态是通过给它赋予一个特殊值`nil`来完成的：</del>
通过给可选变量赋予特殊值`nil`来表示没有值的状态：

```
var serverResponseCode: Int? = 404
// serverResponseCode contains an actual Int value of 404
serverResponseCode = nil
// serverResponseCode now contains no value
```

> NOTE

> nil cannot be used with non-optional constants and variables. If a constant or variable in your code needs to be able to cope with the absence of a value under certain conditions, always declare it as an optional value of the appropriate type.

> 注意

> `nil`不能被用于可选类型之外的常量和变量。如果你的代码中的常量或变量需要处理值缺失的情况，总是用一个可选的合适类型来声明它。

If you define an optional constant or variable without providing a default value, the constant or variable is automatically set to nil for you:

如果你定义一个可选的常量或变量，却没有赋初值，这个常量或变量会自动设*置*为`nil`：

```
var surveyAnswer: String?
// surveyAnswer is automatically set to nil
```

> NOTE

> Swift’s nil is not the same as nil in Objective-C. In Objective-C, nil is a pointer to a non-existent object. In Swift, nil is not a pointer—it is the absence of a value of a certain type. Optionals of any type can be set to nil, not just object types.

> 注意

> Swift的`nil`和Objective-C中的不完全一样。Objective-C中，`nil`是指向不存在<del>的</del>对象*的指针*。而在Swift中，`nil`不<del>知</del>止是一个指针——它是一个特定类型的值缺失。可选的任何类型都可以设为`nil`，不只是对象类型。

## Implicitly Unwrapped Optionals
## 隐式解析可选值

As described above, optionals indicate that a constant or variable is allowed to have “no value”. Optionals can be checked with an if statement to see if a value exists, and can be conditionally unwrapped with optional binding to access the optional’s value if it does exist.

像之前说的，可选值意味着一个常量或变量允许“没有值”。可以通过`if`语句来判断可选值中是否有值存在，如果值存在则用可选值绑定来调用可选量的值。

Sometimes it is clear from a program’s structure that an optional will always have a value, after that value is first set. In these cases, it is useful to remove the need to check and unwrap the optional’s value every time it is accessed, because it can be safely assumed to have a value all of the time.

有时候从程序的结构可以清楚的知道一个可选值在第一次值设定之后，它总是有值的。在这些情况下，把每次调用都检查并解析可选量的值去掉是很有用的，因为它们可以安全的被推断出它们总是有值的。

These kinds of optionals are defined as implicitly unwrapped optionals. You write an implicitly unwrapped optional by placing an exclamation mark (String!) rather than a question mark (String?) after the type that you want to make optional.

这些类型的可选值被定义为隐式解析可选值。当你创建可选值的时候，你可以通过写感叹号(String!)而不是问号(String?)的形式来<del>写</del>表示一个隐式解析的可选值。

Implicitly unwrapped optionals are useful when an optional’s value is confirmed to exist immediately after the optional is first defined and can definitely be assumed to exist at every point thereafter. The primary use of implicitly unwrapped optionals in Swift is during class initialization, as described in Unowned References and Implicitly Unwrapped Optional Properties.

如果可选值在第一次定义之后就肯定存在值并且之后每一刻都肯定存在，这种情况下隐式解析可选值是很有用<del>红</del>的。Swift中的隐式解析可选值的主要用法是在类的初始化过程中，参见[Unowned References and Implicitly Unwrapped Optional Properties](link)。

An implicitly unwrapped optional is a normal optional behind the scenes, but can also be used like a nonoptional value, without the need to unwrap the optional value each time it is accessed. The following example shows the difference in behavior between an optional String and an implicitly unwrapped optional String:

一个隐式解析可选值其实是一个普通的可选值，但它也可以像非可选的值那样使用，无须每次调用都解析可选量的值。下面的例子显示了一个普通的可选的字符串和一个隐式解析的可选字符串的区别：

```
let possibleString: String? = "An optional string."
println(possibleString!) // requires an exclamation mark to access its value
// prints "An optional string."

let assumedString: String! = "An implicitly unwrapped optional string."
println(assumedString)  // no exclamation mark is needed to access its value
// prints "An implicitly unwrapped optional string."
```

You can think of an implicitly unwrapped optional as giving permission for the optional to be unwrapped automatically whenever it is used. Rather than placing an exclamation mark after the optional’s name each time you use it, you place an exclamation mark after the optional’s type when you declare it.

你可以把隐式解析可选值当作一个允许可选值每次都能自动解析的授权。你只需要当你声明的时候在可选量的类型后面放一个感叹号，而不用每次使用的时候都在可选值后面放感叹号。

> NOTE

> If you try to access an implicitly unwrapped optional when it does not contain a value, you will trigger a runtime error. The result is exactly the same as if you place an exclamation mark after a normal optional that does not contain a value.

> 注意

> 如果你试图调用一个没有值的隐式解析可选值，你会得到一个<del>实时的</del>运行时错误。这和你在一个普通的不含值的可选值后面放感叹号的结果是完全一样的。

You can still treat an implicitly unwrapped optional like a normal optional, to check if it contains a value:

你仍然可以把隐式解析可选值当作一个普通的可选值，来检查它是否含有值：

```
if assumedString {
    println(assumedString)
}
// prints "An implicitly unwrapped optional string."
```

You can also use an implicitly unwrapped optional with optional binding, to check and unwrap its value in a single statement:

你同样可以对隐式解析可选值使用可选值绑定，在一行声明中来检查和解析它的值：

```
if let definiteString = assumedString {
    println(definiteString)
}
// prints "An implicitly unwrapped optional string."
```

> NOTE

> Implicitly unwrapped optionals should not be used when there is a possibility of a variable becoming nil at a later point. Always use a normal optional type if you need to check for a nil value during the lifetime of a variable.

> 注意

> 当一个变量有可能是`nil`的情况下，不应当使用隐式解析可选值。如果在整个过程中检查一个变量是否有`nil`值，你应该用一个普通的可选值。

# Assertions
# 断言

Optionals enable you to check for values that may or may not exist, and to write code that copes gracefully with the absence of a value. In some cases, however, it is simply not possible for your code to continue execution if a value does not exist, or if a provided value does not satisfy certain conditions. In these situations, you can trigger an assertion in your code to end code execution and to provide an opportunity to debug the cause of the absent or invalid value.

可选值让你可以检查一个值是否存在，并且优雅的处理值缺失的情况。然而，在一些情况下，如果值不存在或者值不满足指定的条件，你的程序就无法继续执行。在这些情况下，你可以在代码中触发一个断言，来中断代码的执行<del>并且提供一个</del>来调试为什么值缺失或无效<del>的机会</del>。

## Debugging with Assertions
## 用断言来调试

An assertion is a runtime check that a logical condition definitely evaluates to true. Literally put, an assertion “asserts” that a condition is true. You use an assertion to make sure that an essential condition is satisfied before executing any further code. If the condition evaluates to true, code execution continues as usual; if the condition evaluates to false, code execution ends, and your app is terminated.

断言是判断一个逻辑条件是否为真的实时检查。基本上，一个断言就是“断定”（asserts）一个条件为真。你可以使用断言来确保在运行后续代码之前<del>它的</del>一个必要的条件是已经满足了的。如果这个条件为真，代码会正常执行，如果条件为否，代码会停止执行，并且你的<del>app</del>应用会终止。

If your code triggers an assertion while running in a debug environment, such as when you build and run an app in Xcode, you can see exactly where the invalid state occurred and query the state of your app at the time that the assertion was triggered. An assertion also lets you provide a suitable debug message as to the nature of the assert.

如果你的代码<del>值</del>在调试环境下触发了一个断言<del>，</del>（比如当你在Xcode中创建并运行一个app的时候），你可以准确的看到非法语句出现的位置，也可以查询到当断言触发时app的状态。断言还允许你可以提供一个相应的调试信息。

You write an assertion by calling the global assert function. You pass the assert function an expression that evaluates to true or false and a message that should be displayed if the result of the condition is false:

通过调用全局的<del>断言</del>assert函数来写一个断言。你给断言函数传入一个<del>等于true或false的表达式</del>会被解析为`true`或者`false`的表达式，<del>当结果是false的时候，会显示出一条信息</del>以及在解析为`false`时的提示信息：

```
let age = -3
assert(age >= 0, "A person's age cannot be less than zero")
// this causes the assertion to trigger, because age is not >= 0
```

In this example, code execution will continue only if age >= 0 evaluates to true, that is, if the value of age is non-negative. If the value of age is negative, as in the code above, then age >= 0 evaluates to false, and the assertion is triggered, terminating the application.

在这个例子里，只有`age >= 0`为真的时候代码才会继续执行，也就是，如果`age`的值是非负数。在上面的代码中，如果`age`的值是负数，<del>在上面的代码中，</del>`age >= 0`<del>的条件判断</del>这个表达式解析为否，<del>这个</del>断言被触发，终止了这个程序。

Assertion messages cannot use string interpolation. The assertion message can be omitted if desired, as in the following example:

断言信息不能使用字符串插值。<del>如果你想，</del>断言信息<del>是</del>可以省略<del>的</del>，像下面这个例子：

```
assert(age >= 0)
```

## When to Use Assertions
## 何时使用断言

Use an assertion whenever a condition has the potential to be false, but must definitely be true in order for your code to continue execution. Suitable scenarios for an assertion check include:

<del>如果</del>在一个条件有可能为否，但只有它为真的时候代码才能继续执行<del>，这时</del>时，应该使用断言。<del>适当的</del>使用断言检查的*合适*场景包括：

- An integer subscript index is passed to a custom subscript implementation, but the subscript index value could be too low or too high.
- A value is passed to a function, but an invalid value means that the function cannot fulfill its task.
- An optional value is currently nil, but a non-nil value is essential for subsequent code to execute successfully.

- 一个整数类型的下标索引被传入一个自定义的下标实现，但是这个下标索引值太小或太大。
- 一个值传入一个函数，但是如果传入不合法的值，这个函数就无法满足需求。
- 一个可选值当前的值是`nil`，但是后续代码成功执行需要一个非`nil`值。

See also Subscripts and Functions.

参见[Subscripts and Functions](link)。

> NOTE

> Assertions cause your app to terminate and are not a substitute for designing your code in such a way that invalid conditions are unlikely to arise. Nonetheless, in situations where invalid conditions are possible, an assertion is an effective way to ensure that such conditions are highlighted and noticed during development, before your app is published.

> 注意

> 断言会造成你的app终止，它并不能代替你设计代码来保证不合法情况不出现。尽管如此，当不合法的情况可能出现时，断言可以有效的保证在你的app正式发布之前<del>，在</del>的开发过程中这种不合法的情况就会被高亮并被注意到。