## 字符和字符串


A string is an ordered collection of characters, such as "hello, world" or "albatross". Swift strings are represented by the String type, which in turn represents a collection of values of Character type.

字符串指的是一组字符的有序集合[to: 字符串指的是一组有序的字符集合]，比如「hello, world」或者「albatoross」。<s>在 Swift 里，字符串通过 `String` 类型表示，或者从另外一个角度来说，它是一组 `Character` 对象的值的集合</s> [to: Swift 中的字符串用 `String` 类型来表示，反过来说，它是一组 `Character` 类型的值集]。



Swift’s String and Character types provide a fast, Unicode-compliant way to work with text in your code. The syntax for string creation and manipulation is lightweight and readable, with a similar syntax to C strings. String concatenation is as simple as adding together two strings with the + operator, and string mutability is managed by choosing between a constant or a variable, just like any other value in Swift.

Swift 的 `String` 和 `Character` 类型为代码里的字符操作提供了一种快速的、兼容 Unicode 的途径。跟 C 语言类似，在 Swift 里面新建和操作字符的语法十分简单易读。<s>字符串的合并只需要在两个字符串中间见天一个 `+` 运算符，同时就像其它 Swift 值一样，可以通过定义字符串为常量或是变量来决定它是否可被修改。</s> [to:字符串合并就像用`+`操作符相加两个字符串那么简单，另外，就像Swift里的其他值，可以通过定义字符串为常量还是变量来设置它是否可被修改。]


Despite this simplicity of syntax, Swift’s String type is a fast, modern string implementation. Every string is composed of encoding-independent Unicode characters, and provides support for accessing those characters in various Unicode representations.

尽量语法十分简单，Swift 的 `String` 类型是一个快速且现代化的字符串实现。<s>每个字符串都由一组独立编码的 Unicode 字符组成，并且对这些字符提供了多种可访问的 Unicode 编码形式。</s> [to:每个字符串由一组独立编码的 Unicode 字符组成，并提供了这些字符的多种可访问 Unicode 编码形式。]

Strings can also be used to insert constants, variables, literals, and expressions into longer strings, in a process known as string interpolation. This makes it easy to create custom string values for display, storage, and printing.

[to:字符串还可以通过字符串插值这种方式插入常量、变量、字面量或表达式来变得更长。这使得创建用来展示、存储和打印的自定义字符串值变得简单。]

> #### NOTE
> 
> Swift’s String type is bridged seamlessly to Foundation’s NSString class. If you are working with the Foundation framework in Cocoa or Cocoa Touch, the entire NSString API is available to call on any String value you create, in addition to the String features described in this chapter. You can also use a String value with any API that requires an NSString instance.
> 
> For more information about using String with Foundation and Cocoa, see Using Swift with Cocoa and Objective-C.

> #### 需要注意

> Swift 的 `String` 类型无缝接入了 Foundation 的 `NSString` 类。如果你之前在 Cocoa 或 Cocoa Touch 中使用了 Foundation 框架，所有 `NSString` 的 API 都可以用在新的 `String` 实例对象上，而且 `String` 对象还额外添加了下文中提到的特性。同时也可以把 `String` 对象用在任何需要传入 `NSString` 实例为参数的 API 中。

> 更多关于 `String` 和 Foundation 或 Coca 使用方法的信息，请查看 [Using Swift with Cocoa and Objective-C]()。

### String Literals

### 字符串字面量

You can include predefined String values within your code as string literals. A string literal is a fixed sequence of textual characters surrounded by a pair of double quotes ("").

<s>我们可以在代码的前面先定义一些字符串字面量。</s> [to: 我们可以在代码中预定义`Sting`值为*字符串字面量*。] <s>字符串字面量是由一对引号（""）包裹的含有相对顺序的字符集合。</s>[to: 字符串字面量是由一对引号（`""`）包围的固定文本字符序列。]

A string literal can be used to provide an initial value for a constant or variable:

字符串字面量可以给常量或者变量<s>提供一个初始值</s>[to:提供初始值]：

	let someString = "Some string literal value"

Note that Swift infers a type of String for the someString constant, because it is initialized with a string literal value.
	
需要注意的是，Swift 会自动把 `someString` 定义为 `String` 类型，因为它的初始值是一个字符串字面量。


String literals can include the following special characters:

字符串字面量可以包含以下特殊字符：

* The escaped special characters \0 (null character), \\ (backslash), \t (horizontal tab), \n (line feed), \r (carriage return), \" (double quote) and \' (single quote)
* Single-byte Unicode scalars, written as \xnn, where nn is two hexadecimal digits
* Two-byte Unicode scalars, written as \unnnn, where nnnn is four hexadecimal digits
* Four-byte Unicode scalars, written as \Unnnnnnnn, where nnnnnnnn is eight hexadecimal digits

* 转义后的特殊字符 `\0`（空字符），`\\`（斜杠），`\t`（水平 Tab），`\n`（换行），`\r`（回车），`\"`（双引号），`\'`（单引号）；
* 单字节 Unicode 字符，一般写为 `\xnn`，其中 `nn` 是两位十六进制数值；
* 双字节 Unicode 字符，一般写为 `\unnnn`，其中 `nnnn` 是四位十六进制数值；
* 四字节 Unicode 字符，一般写为 `\Unnnnnnnn`，其中 `nnnnnnnn` 是八个十六进制数值；

The code below shows an example of each kind of special character. The wiseWords constant contains two escaped double quote characters. The dollarSign, blackHeart, and sparklingHeart constants demonstrate the three different Unicode scalar character formats:

下面的代码中，<s>对各种特殊字符举了一些例子</s>[to：给每种特殊字符各举了一个例子]。`wiseWords` 常量包含了两个被转义的引号字符。`dollarSign`、`blackHeart` 和 `sparklingHeart` 常量展示了三种不同类型的 Unicode 字符表示方式。

	let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
	// "Imagination is more important than knowledge" - Einstein
	let dollarSign = "\x24"        // $,  Unicode 字符 U+0024
	let blackHeart = "\u2665"      // ♥,  Unicode 字符 U+2665
	let sparklingHeart = "\U0001F496"  // 💖, Unicode 字符 U+1F496

### Initializing an Empty String

### 初始化字符串

To create an empty String value as the starting point for building a longer string, either assign an empty string literal to a variable, or initialize a new String instance with initializer syntax:

	var emptyString = ""               // empty string literal
	var anotherEmptyString = String()  // initializer syntax
	// these two strings are both empty, and are equivalent to each other

一般我们会初始化一个<s>空白的字符串</s>[to:空字符串]作为后面组装长字符串的基础，Swift 提供了两种初始化字符串的方式，第一种是给变量赋予一个<s>空白的字符串字面量</s>[to:空字符串字面量]，第二种是通过新建实例的语法：


	var emptyString = ""               // 空白的字符串字面量
	var anotherEmptyString = String()  // 新建 String 实例的语法
	// 这两个字符串都是空白的，而且相互等价。
	
You can find out whether a String value is empty by checking its Boolean isEmpty property:

可以通过 `String` 对象的 `isEmpty` 属性获取一个字符串是否为空，该属性返回的是布尔值：

	if emptyString.isEmpty {
    	println("Nothing to see here")
	}
	// prints "Nothing to see here"


	if emptyString.isEmpty {
    	println("你看不到我")
	}
	// 会输出 "你看不到我"
	

### String Mutability

### 字符串操作

You indicate whether a particular String can be modified (or mutated) by assigning it to a variable (in which case it can be modified), or to a constant (in which case it cannot be modified):

	var variableString = "Horse"
	variableString += " and carriage"
	// variableString is now "Horse and carriage"
 
	let constantString = "Highlander"
	constantString += " and another Highlander"
	// this reports a compile-time error - a constant string cannot be modified


一个字符串是否能被操作取决于它被定义为常量（不能修改）还是变量（允许修改）：

	var variableString = "Horse"
	variableString += " and carriage"
	// 运行后 variableString 将会是 "Horse and carriage"
 
	let constantString = "Highlander"
	constantString += " and another Highlander"
	// 这段代码会在编译时报错，因为常量不能被修改

> #### NOTE

> This approach is different from string mutation in Objective-C and Cocoa, where you choose between two classes (NSString and NSMutableString) to indicate whether a string can be mutated.

> #### 需要注意

> <s>这个地方跟 Objective-C 和 Cocoa 不一致，与前者不同，后者可以使用两种类型的字符串 `NSString` 和 `NSMutableString` 来区分该字符是否能被修改</s>[to:这种方式与 Objective-C 和 Cocoa 有所不同，这两者通过设置字符串为 `NSString` 还是 `NSMutableString` 来区分该字符是否能被修改]。


### Strings Are Value Types

### 字符串是值类型

Swift’s String type is a value type. If you create a new String value, that String value is copied when it is passed to a function or method, or when it is assigned to a constant or variable. In each case, a new copy of the existing String value is created, and the new copy is passed or assigned, not the original version. Value types are described in Structures and Enumerations Are Value Types.


Swift 中的 `String` 类型属于*值类型*，也就是说你一旦把一个字符串<s>传进一个方法或者函数里面</s>[to:传给一个方法或函数]，或者重新赋值<s>到</s>[to:给]一个新的常量或变量时，字符串的值都会被复制一遍。<s>详细来说就是</s>[to:在以上每种情况中，]，String 类型会把原来的字符串复制为一个新的拷贝，再进行传递和分配，<s>传递后的字符串已经不是原来的那个</s>[to:传递的字符串不是最初的那个]。关于值类型的详细介绍<s>会在</s>[to:请参见] [Structures and Enumerations Are Value Types]()。


> #### NOTE

> This behavior differs from that of NSString in Cocoa. When you create an NSString instance in Cocoa, and pass it to a function or method or assign it to a variable, you are always passing or assigning a reference to the same single NSString. No copying of the string takes place, unless you specifically request it.

> ### 需要注意

> 这个行为和 Cocoa 里的 `NSString` 有所 <s>区别</s>[to:不同]。<s>每</s> 当实例化一个 `NSString` 对象之后，<s>无论怎么在函数和方法之间传递，它都只是指向原来的值的引用</s>[to:无论是把它传递给一个函数或方法，还是把它赋值给一个变量，我们传递或者赋值的是一个指向同一个 `NSString` 的引用]。<s>并不会每次复制这个字符串对象，除非你主动要求这么做</s>[to:除非我们特别要求，否则不会复制这个字符串对象]。


Swift’s copy-by-default String behavior ensures that when a function or method passes you a String value, it is clear that you own that exact String value, regardless of where it came from. You can be confident that the string you are passed will not be modified unless you modify it yourself.

Swift 这种默认复制的行为确保了每个方法或者函数里面接收到的字符串都完全属于这个方法或函数的，并不需要考虑它从哪来，<s>这样就保证了字符串不会变动，除非主动修改它</s>[to:这样就使得我们能够确保传递的字符串不会被修改，除非我们主动去修改它]。

Behind the scenes, Swift’s compiler optimizes string usage so that actual copying takes place only when absolutely necessary. This means you always get great performance when working with strings as value types.

实际上，Swift 的编译器优化了字符串的使用 <s>过程</s>，只有绝对需要时才会产生复制的实际操作。这样就意味着 Swift 可以在字符串操作上和值类型保持一样的高性能。


### Working with Characters

### 字符处理

Swift’s String type represents a collection of Character values in a specified order. Each Character value represents a single Unicode character. You can access the individual Character values in a string by iterating over that string with a for-in loop:

Swift 的 `String` 类型<span>是由一系列 `Character` 对象根据一定的顺序排列组成的</s>[to:是一组有着特定顺序的 `Character` 序列]。每个 `Character` <s>对象都对应着</s>[to:代表了]一个 Unicode 字符。我们可以用<s>一个</s> `for-in` 循环逐个读取字符串中的 `Character` <s>对象</s>[to:值]：

	for character in "Dog!🐶" {
    	println(character)
	}
	// D
	// o
	// g
	// !
	// 🐶


The for-in loop is described in For Loops.

`for-in` 循环的<s>介绍在</s>[to:介绍请参见] [For Loops]()。

Alternatively, create a stand-alone Character constant or variable from a single-character string literal by providing a Character type annotation:

此外，可以通过为一个单独的字符指定 `Character` 类型去定义一个独立的 `Character` 常量或者变量<s></s>[to:可以通过 `Character`类型声明单字符变量或常量]：

	let yenSign: Character = "¥"
	

### Counting Characters

### 计算字符个数

To retrieve a count of the characters in a string, call the global countElements function and pass in a string as the function’s sole parameter:

	let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
	println("unusualMenagerie has \(countElements(unusualMenagerie)) characters")
	// prints "unusualMenagerie has 40 characters"

如果需要计算一个字符串中字符的数量，可以 <s>通过</s> 调用全局方法 `countElements` 并把该字符串作为唯一的参数：

	let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
	println("unusualMenagerie 拥有 \(countElements(unusualMenagerie)) 个字符")
	// hui输出 "unusualMenagerie 拥有 40 个字符"


> #### NOTE

> Different Unicode characters and different representations of the same Unicode character can require different amounts of memory to store. Because of this, characters in Swift do not each take up the same amount of memory within a string’s representation. As a result, the length of a string cannot be calculated without iterating through the string to consider each of its characters in turn. If you are working with particularly long string values, be aware that the countElements function must iterate over the characters within a string in order to calculate an accurate character count for that string.

> Note also that the character count returned by countElements is not always the same as the length property of an NSString that contains the same characters. The length of an NSString is based on the number of 16-bit code units within the string’s UTF-16 representation and not the number of Unicode characters within the string. To reflect this fact, the length property from NSString is called utf16count when it is accessed on a Swift String value.


> #### 需要注意

> 不同的 Unicdoe 字符或者同一个 Unicode 字符的不同表示方式可能需要不同的内存大小进行存储。因此，<s>在一个字符串中每个字符</s>[to:一个字符串中的各个字符]可能占用不同的内存大小。<s>结果导致</s>[to:因此，]如果需要知道一个字符串的长度，必须通过<s>迭代</s>[to:遍历]整个字符串中的字符才能计算出来。如果我们在处理一个超长字符串，必须要注意的是 `countElements` 方法会<s>迭代</s>[to:遍历]整个字符串来精确计算该字符串的长度。

> 另外需要注意的是，对于同一个字符串，通过执行 `countElements` 方法返回的字符串数量不一定和 `NSString` 使用 `length` 属性得到的值一样。因为 `NSString` 的 `length` 值是基于 `UTF-16` 十六位编码方式[to:中的16位编码单元的数量来]统计的，<s>并未直接统计字符串里 Unicode 字符的数量</s>[to:而不是字符串里的 Unicode 字符的数量]。为了反映这个事实，Swift 里 `String` 对象的 `utf16count` 属性对应 `NSString` 类的 `length` 值。


### Concatenating Strings and Characters

### 字符和字符串的拼接

String and Character values can be added together (or concatenated) with the addition operator (+) to create a new String value:

	let string1 = "hello"
	let string2 = " there"
	let character1: Character = "!"
	let character2: Character = "?"
 
	let stringPlusCharacter = string1 + character1        // equals "hello!"
	let stringPlusString = string1 + string2              // equals "hello there"
	let characterPlusString = character1 + string1        // equals "!hello"	let characterPlusCharacter = character1 + character2  // equals "!?"

`String` 和 `Character` 对象可以通过 `+` 运算符进行组合（或者拼接），从而产生一个新的 `String` 对象：


	let string1 = "hello"
	let string2 = " there"
	let character1: Character = "!"
	let character2: Character = "?"
 
	let stringPlusCharacter = string1 + character1        // 等于 "hello!"
	let stringPlusString = string1 + string2              // 等于 "hello there"
	let characterPlusString = character1 + string1        // 等于 "!hello"	let characterPlusCharacter = character1 + character2  // 等于 "!?"


You can also append a String or Character value to an existing String variable with the addition assignment operator (+=):

	var instruction = "look over"
	instruction += string2
	// instruction now equals "look over there"
 
	var welcome = "good morning"
	welcome += character1
	// welcome now equals "good morning!"

也可以通过加法赋值运算符 `+=` 在一个已有的 `String` 变量后面追加 `String` 或 `Character` 对象：

	var instruction = "look over"
	instruction += string2
	// instruction 现在是 "look over there"
 
	var welcome = "good morning"
	welcome += character1
	// welcome now 现在是 "good morning!"

> #### NOTE

> You can’t append a String or Character to an existing Character variable, because a Character value must contain a single character only.

> #### 需要注意

> 无法在 `Character` 对象后面追加任何 `String` 或 `Character` 字符，因为 `Character` 对象必须只有一个字符。


### String Interpolation

### 字符串插值

String interpolation is a way to construct a new String value from a mix of constants, variables, literals, and expressions by including their values inside a string literal. Each item that you insert into the string literal is wrapped in a pair of parentheses, prefixed by a backslash:

	let multiplier = 3
	let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
	// message is "3 times 2.5 is 7.5"


字符串插值是一种新的创建 `String` 对象的方式，它可以在字符串中插入一系列的常量、变量、字面量和包含值运算的表达式。每种插值在字符串中必须用以斜线 `\` 打头并用圆括号 `()` 包裹起来：

	let multiplier = 3
	let message = "\(multiplier) 的 2.5 倍是 \(Double(multiplier) * 2.5)"
	// 运行后输出 "3 的 2.5 倍是 7.5"
	
In the example above, the value of multiplier is inserted into a string literal as \(multiplier). This placeholder is replaced with the actual value of multiplier when the string interpolation is evaluated to create an actual string.

在上面的例子中，`multiplier` 的值以 `\(multiplier)` 的方式插入到字符串中，这个占位符会在字符串进行插值运算时自动替换成 `multiplier` 实际的值。

The value of multiplier is also part of a larger expression later in the string. This expression calculates the value of Double(multiplier) * 2.5 and inserts the result (7.5) into the string. In this case, the expression is written as \(Double(multiplier) * 2.5) when it is included inside the string literal.

`multiplier` 同时也在字符串后面的表达式中出现，这个表达式会被执行并把计算结果（7.5）插入到字符串中。在这个案例里面，<s>该表达式被写成了 `\(Double(multiplier) * 2.5)` 并插在了字符串里面</s>[to: 当被包含在字符串字面量中时，该表达式被写为 `\(Double(multiplier) * 2.5)`]。


### Comparing Strings

### 字符串比较

Swift provides three ways to compare String values: string equality, prefix equality, and suffix equality.

Swift 提供了三种对比字符串的方式：全值比较、前缀比较和后缀比较。

#### String Equality

#### 全值比较

Two String values are considered equal if they contain exactly the same characters in the same order:

	let quotation = "We're a lot alike, you and I."
	let sameQuotation = "We're a lot alike, you and I."
	if quotation == sameQuotation {
    	println("These two strings are considered equal")
	}
	// prints "These two strings are considered equal"



如果两个字符串<s>由相同的字符和一致的顺序组成</s>[to:包含的字符完全相同，并且这些字符的排列顺序也相同]，那就认为这两个字符串是完全相等的：

	let quotation = "We're a lot alike, you and I."
	let sameQuotation = "We're a lot alike, you and I."
	if quotation == sameQuotation {
    	println("这两个字符串是相等的")
	}
	// 运行后会输出 "这两个字符串是相等的"
	
#### Prefix and Suffix Equality

#### 前缀比较和后缀比较

To check whether a string has a particular string prefix or suffix, call the string’s hasPrefix and hasSuffix methods, both of which take a single argument of type String and return a Boolean value. Both methods perform a character-by-character comparison between the base string and the prefix or suffix string.

通过调用字符串的 `hasPrefix` 或 `hasSuffix` [to:方法]来判断该字符串是否含有特定的前缀或后缀，这两个方法<s>分别</s>都接收一个字符串参数，<s>结果</s>[to:并]返回布尔值。这两个方法会在字符串和需要对比的前缀或后缀进行逐字对比。

The examples below consider an array of strings representing the scene locations from the first two acts of Shakespeare’s Romeo and Juliet:

	let romeoAndJuliet = [
    	"Act 1 Scene 1: Verona, A public place",
    	"Act 1 Scene 2: Capulet's mansion",
    	"Act 1 Scene 3: A room in Capulet's mansion",
    	"Act 1 Scene 4: A street outside Capulet's mansion",
    	"Act 1 Scene 5: The Great Hall in Capulet's mansion",
    	"Act 2 Scene 1: Outside Capulet's mansion",
    	"Act 2 Scene 2: Capulet's orchard",
    	"Act 2 Scene 3: Outside Friar Lawrence's cell",
    	"Act 2 Scene 4: A street in Verona",
    	"Act 2 Scene 5: Capulet's mansion",
    	"Act 2 Scene 6: Friar Lawrence's cell"
	]

下面的例子来自莎士比亚著作的《罗密欧与茱丽叶》，我们用前两场戏每一幕对应的地点组成一个数组：

	let romeoAndJuliet = [
    	"Act 1 Scene 1: Verona, A public place",
    	"Act 1 Scene 2: Capulet's mansion",
    	"Act 1 Scene 3: A room in Capulet's mansion",
    	"Act 1 Scene 4: A street outside Capulet's mansion",
    	"Act 1 Scene 5: The Great Hall in Capulet's mansion",
    	"Act 2 Scene 1: Outside Capulet's mansion",
    	"Act 2 Scene 2: Capulet's orchard",
    	"Act 2 Scene 3: Outside Friar Lawrence's cell",
    	"Act 2 Scene 4: A street in Verona",
    	"Act 2 Scene 5: Capulet's mansion",
    	"Act 2 Scene 6: Friar Lawrence's cell"
	]

You can use the hasPrefix method with the romeoAndJuliet array to count the number of scenes in Act 1 of the play:

	var act1SceneCount = 0
	for scene in romeoAndJuliet {
    	if scene.hasPrefix("Act 1 ") {
        	++act1SceneCount
    	}
	}
	println("There are \(act1SceneCount) scenes in Act 1")
	// prints "There are 5 scenes in Act 1"

我们可以用 `hasPrefix` 方法统计在 `romeoAndJuliet` 数组中第一场戏一共有几幕：

	var act1SceneCount = 0
	for scene in romeoAndJuliet {
    	if scene.hasPrefix("Act 1 ") {
        	++act1SceneCount
    	}
	}
	println("第一场戏一共有 \(act1SceneCount) 幕")
	// 运行后输出： "第一场戏一共有 5 幕"

Similarly, use the hasSuffix method to count the number of scenes that take place in or around Capulet’s mansion and Friar Lawrence’s cell:

	var mansionCount = 0
	var cellCount = 0
	for scene in romeoAndJuliet {
    	if scene.hasSuffix("Capulet's mansion") {
        	++mansionCount
    	} else if scene.hasSuffix("Friar Lawrence's cell") {
        	++cellCount
    	}
	}
	println("\(mansionCount) mansion scenes; \(cellCount) cell scenes")
	// prints "6 mansion scenes; 2 cell scenes"


类似地，用 `hasSuffix` 方法来统计发生在 `Capulet's mansion` 和 `Friar Lawrence's cell` 场景的数量：

	var mansionCount = 0
	var cellCount = 0
	for scene in romeoAndJuliet {
    	if scene.hasSuffix("Capulet's mansion") {
        	++mansionCount
    	} else if scene.hasSuffix("Friar Lawrence's cell") {
        	++cellCount
    	}
	}
	println("\(mansionCount) mansion scenes; \(cellCount) cell scenes")
	// 运行后输出： "6 mansion scenes; 2 cell scenes"


### Uppercase and Lowercase Strings

### 字符串的大小写转换

You can access an uppercase or lowercase version of a string with its uppercaseString and lowercaseString properties:

```
let normal = "Could you help me, please?"
let shouty = normal.uppercaseString
// shouty is equal to "COULD YOU HELP ME, PLEASE?"
let whispered = normal.lowercaseString
// whispered is equal to "could you help me, please?"
```

[to:我们]可以通过字符串<s>本身</s>的 `uppercaseString` 或 `lowercaseString` 属性取得<s>它的全大些或全小写版本</s>[to:某个字符串的大写或小写版本]：


```
let normal = "Could you help me, please?"
let shouty = normal.uppercaseString
// shouty 等价于 "COULD YOU HELP ME, PLEASE?"
let whispered = normal.lowercaseString
// whispered 等价于 "could you help me, please?"
```


### Unicode

### Unicode 字符

Unicode is an international standard for encoding and representing text. It enables you to represent almost any character from any language in a standardized form, and to read and write those characters to and from an external source such as a text file or web page.

`Unicode` 是一个用来编码和表示文本的国际标准。它<s>允许我们用</s> [to: 使得我们可以用] 一个标准格式来表示世界上几乎所有的字符，并且提供了在类似文本文件或网页中读取和写入这些字符的能力。

Swift’s String and Character types are fully Unicode-compliant. They support a number of different Unicode encodings, as described below.

Swift 的 `String` 和 `Character` 类型完全兼容 Unicode ，并且提供了大量 Unicode 编码的支持，下面我们会提到这点。

#### Unicode Terminology

#### Unicode 的术语

Every character in Unicode can be represented by one or more unicode scalars. A unicode scalar is a unique 21-bit number (and name) for a character or modifier, such as U+0061 for LOWERCASE LATIN LETTER A ("a"), or U+1F425 for FRONT-FACING BABY CHICK ("🐥").

Unicode 里的每个字符都对应这一个或多个 uincode 标量。每个 unicode 标量是一个 21 位的数值（包括名称），代表着一个字符或者修饰符。比如 `U+0061` 是 `LOWERCASE LATIN LETTER A ("a")`, `U+1F425` 是 `FRONT-FACING BABY CHICK ("🐥")`。

When a Unicode string is written to a text file or some other storage, these unicode scalars are encoded in one of several Unicode-defined formats. Each format encodes the string in small chunks known as code units. These include the UTF-8 format (which encodes a string as 8-bit code units) and the UTF-16 format (which encodes a string as 16-bit code units).

当一个 Unicode 的字符串被写进文本文件或者其它存储形式时，这些 unicode 标量就会从几种 Unicode 制定的编码方式中选取其中一种把该字符串编码成小块的编码单元。这些编码方式包括了 `UTF-8` 格式（会把字符串编码成 8 位编码单元），`UTF-16` 格式（把字符串编码成 16 位编码单元）。

#### Unicode Representations of Strings

#### Unicode 字符串的表示方式

Swift provides several different ways to access Unicode representations of strings.

<s>Swift 对 Unicode 字符提供了几种不同的访问方式。</s>
[to: Swift 提供了不同的方法来访问字符的Unicode形式。]

You can iterate over the string with a for-in statement, to access its individual Character values as Unicode characters. This process is described in Working with Characters.

<s>首先可以从字符串的逐字迭代中取得每个 `Character` 中的 Unicode 字符。</s>[to: 我们可以用 `for-in`语句遍历字符串来获取到字符串中每个`Character` 相应的 Unicode 字符。] 这个过程在上面的 [字符处理]() 章节中有提到。


Alternatively, access a String value in one of three other Unicode-compliant representations:

```
A collection of UTF-8 code units (accessed with the string’s utf8 property)
A collection of UTF-16 code units (accessed with the string’s utf16 property)
A collection of 21-bit Unicode scalar values (accessed with the string’s unicodeScalars property)
```

另外，还可以通过以下三种 <s>方式中的一种访问字符串中兼容 Unicode 的字符数据</s>[to:统一编码方式来访问一个 `String` 的值]： 

```
一组以 UTF-8 编码的单元 (通过字符串的 utf8 属性访问)
一组以 UTF-16 编码的单元 (通过字符串的 utf16 属性访问)
一组以 21 位编码的单元 (通过字符串的 unicodeScalars 属性访问)
```

Each example below shows a different representation of the following string, which is made up of the characters D, o, g, !, and the 🐶 character (DOG FACE, or Unicode scalar U+1F436):

下面的每个示例 <s>描述了</s>[to: 给出了] 以下字符串<s>不同的几种表示方法</s>[to:的几种不同表示方法]，这个字符串由这几个字符组成：`D`、`o`、`g`、`!` 和 `🐶` 字符（`DOG FACE` 或者 Unicode 标量 `U+1F436`）

```
let dogString = "Dog!🐶"
```


#### UTF-8

You can access a UTF-8 representation of a String by iterating over its utf8 property. This property is of type UTF8View, which is a collection of unsigned 8-bit (UInt8) values, one for each byte in the string’s UTF-8 representation:

我们可以通过 <s>迭代访问</s>[to:遍历] 字符串的 `utf8` 属性来获得该字符串的 `UTF-8` 编码形式。该属性的类型是 `UTF8View`，由一组无符号的<s> 8 位数值（`UInt8`）</s> [to:  8 位（`UInt8`）数值]组成，<s>每个数值代表了字符串用 `UTF-8` 编码后的字节</s>[to：每个字节都是字符串的 UTF-8 编码形式]。

```
for codeUnit in dogString.utf8 {
    print("\(codeUnit) ")
}
print("\n")
// 68 111 103 33 240 159 144 182
```

In the example above, the first four decimal codeUnit values (68, 111, 103, 33) represent the characters D, o, g, and !, whose UTF-8 representation is the same as their ASCII representation. The last four codeUnit values (240, 159, 144, 182) are a four-byte UTF-8 representation of the DOG FACE character.

上面的例子中，前四位十进制的编码单元[to: `(68, 111, 103, 33)`]分别代表了 `D`、`o`、`g`、`!`，这几个字符的编码形式跟 ASCII 是<s>一致的</s>[to:相同的]。最后四位编码单元（240，159，144，182）是<s>一个 4 位的 UTF-8 编码表示形式，用来表示 `DOG FACE` 字符</s>[to: 字符 `DOG FACE` 的 4 位 UTF-8 编码形式]。

#### UTF-16

You can access a UTF-16 representation of a String by iterating over its utf16 property. This property is of type UTF16View, which is a collection of unsigned 16-bit (UInt16) values, one for each 16-bit code unit in the string’s UTF-16 representation:

通过<s>迭代访问</s>[to:遍历]字符串的 `utf16` 属性可以取得该字符串的 `UTF-16` 编码形式，该属性的类型是 `UTF16View`，即一组无符号 <s>16 位数值（UInt16）</s>[to:16 位（UInt16）数值]的集合，<s>每个数值代表了字符串用 `UTF-16` 编码后的字节</s>[to：每个字节都是字符串的 UTF-16 编码形式]。
 
```
for codeUnit in dogString.utf16 {
    print("\(codeUnit) ")
}
print("\n")
// 68 111 103 33 55357 56374
```

Again, the first four codeUnit values (68, 111, 103, 33) represent the characters D, o, g, and !, whose UTF-16 code units have the same values as in the string’s UTF-8 representation.

类似的，前四个编码单元（`68，111，103，33`）代表了<s>前四个</s>字符 `D`、`o`、`g` 和 `!`，这几个字符<s> `UTF-16` 和 `UTF-8` 拥有相同的表示方式</s>[to: 的`UTF-16` 表示方式同 `UTF-8` 的一样]。

The fifth and sixth codeUnit values (55357 and 56374) are a UTF-16 surrogate pair representation of the DOG FACE character. These values are a lead surrogate value of U+D83D (decimal value 55357) and a trail surrogate value of U+DC36 (decimal value 56374).

第五个和第六个`编码单元`（`55357` 和 `56374`）则是 `DOG FACE` 字符的代理项。这两个数值由<s>第一部分的</s> `U+D83D`（十进制 55357） 和 `U+DC36`（十进制 56374）组成。

#### Unicode Scalars

#### Unicode 标量

You can access a Unicode scalar representation of a String value by iterating over its unicodeScalars property. This property is of type UnicodeScalarView, which is a collection of values of type UnicodeScalar. A Unicode scalar is any 21-bit Unicode code point that is not a lead surrogate or trail surrogate code point.

通过<s>迭代</s>[to:遍历]字符串的 `unicodeScalars` 属性可以获得该字符串的 Unicode 标量表示形式。该属性的类型是 `UnicodeScalarView`，由一组 `UnicodeScalar` 类型的值组成。一个 Unicode 标量是一个完整的 21 位编码，既没有首码位，也没有尾码位。

Each UnicodeScalar has a value property that returns the scalar’s 21-bit value, represented within a UInt32 value:

每个 `UnicodeScalar` 都有一个 `value` 属性可以获得它的 21 位（UInt32）标量值：

```
for scalar in dogString.unicodeScalars {
    print("\(scalar.value) ")
}
print("\n")
// 68 111 103 33 128054
```

The value properties for the first four UnicodeScalar values (68, 111, 103, 33) once again represent the characters D, o, g, and !. The value property of the fifth and final UnicodeScalar, 128054, is a decimal equivalent of the hexadecimal value 1F436, which is equivalent to the Unicode scalar U+1F436 for the DOG FACE character.

前四个 `UnicodeScalar` 对象的 `value` 属性值（`68，111，103，33`）按照惯例还是代表着 `D`、`o`、`g` 和 `!` 四个字符。而第五个也就是最后一个 `UnicodeScalar` 数值 128054 的十六进制是 1F436，刚好等价于 `DOG FACE` 字符的 Unicode 标量 `U+1F436` 。

As an alternative to querying their value properties, each UnicodeScalar value can also be used to construct a new String value, such as with string interpolation:

除了使用它们的 `value` 属性，每个 `UnicodeScalar` 对象也可以用来<s>直接</s>构造新的 `String` 对象，比如这里用的字符串插值方法：

```
for scalar in dogString.unicodeScalars {
    println("\(scalar) ")
}
// D
// o
// g
// !
// 🐶
```

