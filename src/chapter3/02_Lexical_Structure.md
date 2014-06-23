# Lexical Structure
# 词法结构

The lexical structure of Swift describes what sequence of characters form valid tokens of the language. These valid tokens form the lowest-level building blocks of the language and are used to describe the rest of the language in subsequent chapters.

Swift的词法结构描述了如何在该语言中用字符序列构建合法标记。这些合法标识构成了该语言最底层的基石，并将会被用于描述后续章节的剩余部分。

In most cases, tokens are generated from the characters of a Swift source file by considering the longest possible substring from the input text, within the constraints of the grammar that are specified below. This behavior is referred to as longest match or maximal munch.

通常，标识将从Swift源文件的输入文本中提取可能的最长子字符串生成。这种方法称为“最长匹配项（longest match）”，或者“最大适合”（maximal munch）。

## Whitespace and Comments
## 空白与注释

Whitespace has two uses: to separate tokens in the source file and to help determine whether an operator is a prefix or postfix (see Operators), but is otherwise ignored. The following characters are considered whitespace: space (U+0020), line feed (U+000A),carriage return (U+000D), horizontal tab (U+0009), vertical tab (U+000B), form feed (U+000C) and null (U+0000).

空白(whitespace)有两个用途：区分源文件中的标识符和帮助确定一个操作符是前缀还是后缀（参见：运算符），否则忽略。以下字符会被认为是空白：s空格（space）（U+0020）、换行符（line feed）（U+000A）、回车符（carriage return）（U+000D）、水平 tab（horizontal tab）（U+0009）、垂直 tab（vertical tab）（U+000B）、换页符（form feed）（U+000C）以及空（null）（U+0000）。

Comments are treated as whitespace by the compiler. Single line comments begin with // and continue until the end of the line. Multiline comments begin with /* and end with */.Nesting is allowed, but the comment markers must be balanced.

注释（comments）被编译器当作空白处理。单行注释以//开始直到该行结束。多行注释由/\*开始，以*/结束。注释允许嵌套，但注释标记必须相匹配。


## Identifiers
## 标识符

Identifiers begin with an upper case or lower case letter A through Z, an underscore (_), a noncombining alphanumeric Unicode character in the Basic Multilingual Plane, or a character outside the Basic Multilingual Plan that isn’t in a Private Use Area. After the first character, digits and combining Unicode characters are also allowed.

标识符以大写或小写字母A到Z，下划线(_)，基本多语言面（Basic Multilingual Plane）中的非组合Unicode字符或者基本多语言面（Basic Multilingual Plane）以外的非专用区（Private Use Area）的字符开始。首字符之后，可以使用数字和 Unicode 字符组合。

To use a reserved word as an identifier, put a backtick (\`) before and after it. For example, class is not a valid identifier, but \`class\` is valid. The backticks are not considered part of the identifier; \`x\` and x have the same meaning.

要使用保留字作为标识符，需要在其前后增加一个反引号(\`)。例如：类不是一个有效的标识符，但`class`是有效的。反引号不会被当做标识符的一部分；`x` 和 x 意义相同。

Inside a closure with no explicit parameter names, the parameters are implicitly named $0, $1, $2, and so on. These names are valid identifiers within the scope of the closure.

闭包（closure）中如果没有明确指定参数名称，参数将被隐式命名为 $0、$1、$2... 这些命名在闭包作用域内是合法的标识符。

> G R A M M A R O F A N I D E N T I F I E R
> 标识符语法

> identifier → identifier-head identifier-characters[opt]

> 标识符 → 标识符头(Head) 标识符字符列表 可选

> identifier → \` identifier-head > identifier-characters[opt] `

> 标识符 → ` 标识符头(Head) 标识符字符列表 可选 `
> 

> identifier → implicit-parameter-name
> 标识符 → 隐式参数名

> identifier-list → identifier identifier , identifier-list

> 标识符列表 → 标识符 | 标识符 , 标识符列表

> identifier-head → Upper- or lowercase letter A through Z

> 标识符头(Head) → Upper- or lowercase letter A through Z

> identifier-head → U+00A8, U+00AA, U+00AD, U+00AF, U+00B2–U+00B5, or
U+00B7–U+00BA

> 标识符头(Head) → U+00A8, U+00AA, U+00AD, U+00AF, U+00B2–U+00B5, or U+00B7–U+00BA

> identifier-head → U+00BC–U+00BE, U+00C0–U+00D6, U+00D8–U+00F6, or
U+00F8–U+00FF

> 标识符头(Head) → U+00BC–U+00BE, U+00C0–U+00D6, U+00D8–U+00F6, or U+00F8–U+00FF


> identifier-head → U+0100–U+02FF, U+0370–U+167F, U+1681–U+180D, or U+180F–
U+1DBF

> 标识符头(Head) → U+0100–U+02FF, U+0370–U+167F, U+1681–U+180D, or U+180F–U+1DBF

> identifier-head → U+1E00–U+1FFF

>标识符头(Head) → U+1E00–U+1FFF

> identifier-head → U+200B–U+200D, U+202A–U+202E, U+203F–U+2040, U+2054, or
U+2060–U+206F

> 标识符头(Head) → U+200B–U+200D, U+202A–U+202E, U+203F–U+2040, U+2054, or U+2060–U+206F


> identifier-head → U+2070–U+20CF, U+2100–U+218F, U+2460–U+24FF, or U+2776–
U+2793

>标识符头(Head) → U+2070–U+20CF, U+2100–U+218F, U+2460–U+24FF, or U+2776–U+2793

> identifier-head → U+2C00–U+2DFF or U+2E80–U+2FFF

> 标识符头(Head) → U+2C00–U+2DFF or U+2E80–U+2FFF

> identifier-head → U+3004–U+3007, U+3021–U+302F, U+3031–U+303F, or U+3040–
U+D7FF

> 标识符头(Head) → U+3004–U+3007, U+3021–U+302F, U+3031–U+303F, or U+3040–U+D7FF

> identifier-head → U+F900–U+FD3D, U+FD40–U+FDCF, U+FDF0–U+FE1F, or
U+FE30–U+FE44

> 标识符头(Head) → U+F900–U+FD3D, U+FD40–U+FDCF, U+FDF0–U+FE1F, or U+FE30–U+FE44

> identifier-head → U+FE47–U+FFFD
> 标识符头(Head) → U+FE47–U+FFFD


> identifier-head → U+10000–U+1FFFD, U+20000–U+2FFFD, U+30000–U+3FFFD, or
U+40000–U+4FFFD

> 标识符头(Head) → U+10000–U+1FFFD, U+20000–U+2FFFD, U+30000–U+3FFFD, or U+40000–U+4FFFD

> identifier-head → U+50000–U+5FFFD, U+60000–U+6FFFD, U+70000–U+7FFFD, or
U+80000–U+8FFFD

> 标识符头(Head) → U+50000–U+5FFFD, U+60000–U+6FFFD, U+70000–U+7FFFD, or U+80000–U+8FFFD

> identifier-head → U+90000–U+9FFFD, U+A0000–U+AFFFD, U+B0000–U+BFFFD, or
U+C0000–U+CFFFD

> 标识符头(Head) → U+90000–U+9FFFD, U+A0000–U+AFFFD, U+B0000–U+BFFFD, or U+C0000–U+CFFFD

> identifier-head → U+D0000–U+DFFFD or U+E0000–U+EFFFD
> 标识符头(Head) → U+D0000–U+DFFFD or U+E0000–U+EFFFD

> identifier-character → Digit 0 through 9

> 标识符字符 → 数值 0 到 9

> identifier-character → U+0300–U+036F, U+1DC0–U+1DFF, U+20D0–U+20FF, or
U+FE20–U+FE2F

> 标识符字符 → U+0300–U+036F, U+1DC0–U+1DFF, U+20D0–U+20FF, or U+FE20–U+FE2F

> identifier-character → identifier-head
> 标识符字符 → 标识符头(Head)

> identifier-characters → identifier-character identifier-characters[opt]
> 标识符字符列表 → 标识符字符 标识符字符列表 可选

> implicit-parameter-name → $ decimal-
> 隐式参数名 → $ 十进制数字列表


## Keywords
## 关键字
The following keywords are reserved and may not be used as identifiers, unless they’re escaped with backticks, as described above in Identifiers.

下述被保留的关键字不允许用作标识符，除非它们被反引号转义，参见标识符。

* Keywords used in declarations: class, deinit, enum, extension, func, import, init, let, protocol,static, struct, subscript, typealias, and var.
* 用作声明的关键字：class、deinit、enum、extension、func、import、init、let、protocol、static、struct、subscript、typealias、var

* Keywords used in statements: break, case, continue, default, do, else, fallthrough, if, in, for,return, switch, where, and while.

* 用作语句的关键字：break、case、continue、default、do、else、fallthrough、if、in、for、return、switch、where、while

* Keywords used in expressions and types: as, dynamicType, is, new, super, self, Self, Type,__COLUMN__, __FILE__, __FUNCTION__, and __LINE__.

* 用作表达和类型的关键字：as、dynamicType、is、new、super、self、Self、Type、__COLUMN__、__FILE__、__FUNCTION__、__LINE__

* Keywords reserved in particular contexts: associativity, didSet, get, infix, inout, left, mutating,none, nonmutating, operator, override, postfix, precedence, prefix, right, set, unowned, unowned(safe),unowned(unsafe), weak and willSet. Outside the context in which they appear in the grammar, they can be used as identifiers.

* 特定上下文中被保留的关键字：associativity、didSet、get、infix、inout、left、mutating、none、nonmutating、operator、override、postfix、precedence、prefix、right、set、unowned、unowned(safe)、unowned(unsafe)、weak、willSet，这些关键字在特定上下文之外可以被用于标识符。

## Literals
## 字面量
A literal is the source code representation of a value of an integer, floating-point number, or string type. The following are examples of literals:

字面量在源代码中表示一个整数，浮点数或字符串类型的值。以下是示例：

> 42 // Integer literal

> 3.14159 // Floating-point literal

> "Hello, world!" // String literal

> G R A M M A R O F A L I T E R A L

> literal → integer-literal floating-point-literal string-literal

> 字面量 → 整型字面量 | 浮点数字面量 | 字符串字面量

## Integer Literals
## 整型字面量

Integer literals represent integer values of unspecified precision. By default, integer literals are expressed in decimal; you can specify an alternate base using a prefix. Binary literals begin with 0b, octal literals begin with 0o, and hexadecimal literals begin with 0x.

整型字面量（integer literals）表示未指定精度整型数的值。整型字面量默认为十进制；你可以通过加前缀来改变其数。二进制字面量以 0b 开始，八进制字面量以 0o 开始，十六进制字面量以 0x 开始。

Decimal literals contain the digits 0 through 9. Binary literals contain 0 and 1, octal literalscontain 0 through 7, and hexadecimal literals contain 0 through 9 as well as A through F in upper- or lowercase.

十进制字面量包含数字 0 至 9。二进制字面量只包含 0 或 1，八进制字面量包含数字 0 至 7，十六进制字面量包含数字 0 至 9 以及大写或小写的字母 A 至 F。

Negative integers literals are expressed by prepending a minus sign (-) to an integer literal, as in -42.

负整型字面量的字面量需要在整型字量面前加减号 -，比如 -42。

Underscores (_) are allowed between digits for readability, but are ignored and therefore don’t affect the value of the literal. Integer literals can begin with leading zeros (0), but are likewise ignored and don’t affect the base or value of the literal.

数字间允许使用下划线 _ 来增加可读性，但下划线会被忽略而不会影响字面量的值。整型字面量也可以以0开始，但同样会被忽略而不会影响其基数及字面量的值。

Unless otherwise specified, the default type of an integer literal is the Swift standard library type Int. The Swift standard library also defines types for various sizes of signed and unsigned integers, as described in Integers.

除非特殊指定，整型字面量的默认类型为 Swift 标准库类型中的 Int。Swift 标准库还定义了各种不同长度的是否带符号的整数类型，请参考 整数类型。

> 整型字面量语法
> 整型字面量 → 二进制字面量
> 整型字面量 → 八进制字面量
> 整型字面量 → 十进制字面量
> 整型字面量 → 十六进制字面量
> 二进制字面量 → 0b 二进制数字 二进制字面量字符列表 可选
> 二进制数字 → 数值 0 到 1
> 二进制字面量字符 → 二进制数字 | _
> 二进制字面量字符列表 → 二进制字面量字符 二进制字面量字符列表 可选
> 八进制字面量 → 0o 八进字数字 八进制字符列表 可选
> 八进字数字 → 数值 0 到 7
> 八进制字符 → 八进字数字 | _
> 八进制字符列表 → 八进制字符 八进制字符列表 可选
> 十进制字面量 → 十进制数字 十进制字符列表 可选
> 十进制数字 → 数值 0 到 9
> 十进制数字列表 → 十进制数字 十进制数字列表 可选
> 十进制字符 → 十进制数字 | _
> 十进制字符列表 → 十进制字符 十进制字符列表 可选
> 十六进制字面量 → 0x 十六进制数字 十六进制字面量字符列表 可选
> 十六进制数字 → 数值 0 到 9, a through f, or A through F
> 十六进制字符 → 十六进制数字 | _
> 十六进制字面量字符列表 → 十六进制字符 十六进制字面量字符列表 可选


## Floating-Point Literals
## 浮点型字面量

Floating-point literals represent floating-point values of unspecified precision.

浮点型字面量（floating-point literals）表示未指定精度浮点数的值。

By default, floating-point literals are expressed in decimal (with no prefix), but they can also be expressed in hexadecimal (with a 0x prefix).

浮点型字面量默认用十进制表示（无前缀），但也可以用十六进制表示（加前缀 0x）。

Decimal floating-point literals consist of a sequence of decimal digits followed by either a decimal fraction, a decimal exponent, or both. The decimal fraction consists of a decimal point (.) followed by a sequence of decimal digits. The exponent consists of an upper- or lowercase e prefix followed by sequence of decimal digits that indicates what power of 10 the value preceding the e is multiplied by. For example, 1.25e2 represents 1.25 ⨉ 102, which evaluates to 125.0. Similarly, 1.25e-2 represents 1.25 ⨉ 10-2, which evaluates to 0.0125.

十进制浮点型字面量（decimal floating-point literals）由十进制数字后跟小数部分或指数部分（或两者皆有）组成。十进制小数部分由小数点 . 后跟十进制数字组成。指数部分由大写或小写字母的前缀e 后跟十进制数字组成，这串数字表示 e 之前的数量乘以 10 的几次方。例如：1.25e2 表示 1.25 ⨉ 10^2，也就是 125.0；同样，1.25e－2 表示 1.25 ⨉ 10^－2，也就是 0.0125。

Hexadecimal floating-point literals consist of a 0x prefix, followed by an optional hexadecimal fraction, followed by a hexadecimal exponent. The hexadecimal fraction consists of a decimal point followed by a sequence of hexadecimal digits. The exponent consists of an upper- or lowercase p prefix followed by sequence of decimal digits that indicates what power of 2 the value preceding the p is multiplied by. For example, 0xFp2 represents 15 ⨉ 22, which evaluates to 60. Similarly, 0xFp-2 represents 15 ⨉ 2-2, which evaluates to 3.75.
十六进制浮点型字面量（hexadecimal floating-point literals）由前缀 0x 后跟可选的十六进制小数部分以及十六进制指数部分组成。十六进制小数部分由小数点后跟十六进制数字组成。指数部分由大写或小写字母的前缀p 后跟十进制数字串组成，这串数字表示 p 之前的数量乘以 2 的几次方。例如：0xFp2 表示15 ⨉ 2^2，也就是 60；同样，0xFp-2 表示 15 ⨉ 2^-2，也就是 3.75。

Unlike with integer literals, negative floating-point numbers are expressed by applying the unary minus operator (-) to a floating-point literal, as in -42.0. The result is an expression, not a floating-point integer literal.

与整型字面量不同，负的浮点型字面量由一元运算符减号 - 和浮点型字面量组成，例如 -42.0。这代表一个表达式，而不是一个浮点整型字面量。

Underscores (_) are allowed between digits for readability, but are ignored and therefore don’t affect the value of the literal. Floating-point literals can begin with leading zeros (0),but are likewise ignored and don’t affect the base or value of the literal.

下划线 _ 允许被用于增强可读性，但会被忽略而不影响字面量的值。浮点型字面量也可以在数字前加 0，但同样会被忽略而不影响字面量的值。

Unless otherwise specified, the default type of a floating-point literal is the Swift standard library type Double, which represents a 64-bit floating-point number. The Swift standard library also defines a Float type, which represents a 32-bit floating-point number.

除非特殊指定，浮点型字面量的默认类型为 Swift 标准库类型中的 Double，表示64位浮点数。Swift 标准库也定义 Float 类型，表示32位浮点数。

> 浮点型字面量语法
> 浮点数字面量 → 十进制字面量 十进制分数 可选 十进制指数 可选
> 浮点数字面量 → 十六进制字面量 十六进制分数 可选 十六进制指数
> 十进制分数 → . 十进制字面量
> 十进制指数 → 浮点数e 正负号 可选 十进制字面量
> 十六进制分数 → . 十六进制字面量 可选
> 十六进制指数 → 浮点数p 正负号 可选 十六进制字面量
> 浮点数e → e | E
> 浮点数p → p | P
> 正负号 → + | -

## String Literals
## 字符串型字面量

A string literal is a sequence of characters surrounded by double quotes, with the following form:
字符串型字面量是双引号括起来的一个字符序列，形式如下：

    " characters "
    
String literals cannot contain an unescaped double quote ("), an unescaped backslash (\), a carriage return, or a line feed.
   
字符串型字面量中不能包含未转义的双引号 "、未转义的反斜线\、回车符（carriage return）或换行符（line feed）。

Special characters can be included in string literals using the following escape sequences:
* Null Character (\0)
* Backslash (\\)
* Horizontal Tab (\t)
* Line Feed (\n)
* Carriage Return (\r)
* Double Quote (\")
* Single Quote (\')

特殊符号可以经如下转义后在字符串型字面量中使用：

* 空字符（Null Character）\0
* 反斜线（Backslash）\\
* 水平Tab （Horizontal Tab）\t
* 换行符（Line Feed）\n
* 回车符（Carriage Return）\r
* 双引号（Double Quote）\"
* 单引号（Single Quote）\'

Characters can also be expressed by \x followed by two hexadecimal digits, \u followed by four hexadecimal digits, or \U followed by eight hexadecimal digits. The digits in these escape sequences identify a Unicode codepoint.

字符也可以用以下方式表示：\x 后跟两位十六进制数字，\u 后跟四位十六进制数字，\U 后跟八位十六进制数字。在这些转义序列后跟的数字表示一个Unicode码。

The value of an expression can be inserted into a string literal by placing the expression in parentheses after a backslash (\). The interpolated expression must not contain an unescaped double quote ("), an unescaped backslash (\), a carriage return, or a line feed.

字符串字面量可以在反斜线后面的小括号中插入表达式\（）。插入的表达式必须不能包含未的双引号（”）,反斜线（\）,回车符或换行符。

The expression must evaluate to a value of a type that the String class has an initializer for.

表达式的计算结果必须是String类的一个有初始化的类型的值。

For example, all the following string literals have the same value:
1. “1 2 3"
2. "1 2 \(3)"
3. "1 2 \(1 + 2)"
4. “var x = 3; "1 2 \(x)”

摘录来自: Apple Inc. “The Swift Programming Language”。 iBooks. https://itun.es/cn/jEUH0.l

比如，下面所有的字符串型字面量拥有同样的值：	

"1 2 3"
"1 2 \(3)"
"1 2 \(1 + 2)"
var x = 3; "1 2 \(x)"

The default type of a string literal is String. The characters that make up a string are of type Character. For more information about the String and Character types, see Strings and Characters.

字符串型字面量的默认类型为 String。组成字符串的字符的类型为 Character，更多关于String和Character类型，请参考 字符串和字符。

> 字符型字面量语法
> 字符串型字面量 → " 引用文本 "
> 引用文本 → 引用文本条目 引用文本 可选
> 引用文本条目 → 转义字符
> 引用文本条目 → ( 表达式 )
> 引用文本条目 → 除了"¬, \¬, U+000A, or U+000D的所有Unicode的字符
> 转义字符 → \0 | \ | \t | \n | \r | \" | \'
> 转义字符 → \x 十六进制数字 十六进制数字
> 转义字符 → \u 十六进制数字 十六进制数字 十六进制数字 十六进制数字
> 转义字符 → \U 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字

## Operators
## 运算符

The Swift standard library defines a number of operators for your use, many of which are discussed in Basic Operators and Advanced Operators. The present section describes which characters can be used as operators.

Swift标准库定义了许多供你使用的运算符，其中大部分将在 基础运算符 和 高级运算符 中进行阐述。本章节将描述了哪些字符可被用作运算符。

Operators are made up of one or more of the following characters: /, =, -, +, !, *, %, <, >,&, |, ^, ~, and .. That said, the tokens =, ->, //, /*, */, ., and the unary prefix operator & are reserved. These tokens can’t be overloaded, nor can they be used to define custom operators.

运算符由一个或多个如下字符组成：/、=、-、+、!、*、%、<、>、&、|、^、~、.。也就是说，标记 =,->、//、/*、*/、. 以及一元前缀运算符 & 属于保留字，这些标记不能被重写或用于定义自定义的运算符。

The whitespace around an operator is used to determine whether an operator is used as a prefix operator, a postfix operator, or a binary operator. This behavior is summarized in the following rules:

运算符两侧的空白被用来区分一个运算符是否被用为前缀运算符（prefix operator）、后缀运算符（postfix operator）或二元运算符（binary operator）。规则总结如下：

* If an operator has whitespace around both sides or around neither side, it is
treated as a binary operator. As an example, the + operator in a+b and a + b is
treated as a binary operator.

* 如果运算符两侧都有空白或两侧都无空白，将被看作二元运算符。例如：a+b 和 a + b 中的运算符+ 被看作二元运算符。

* If an operator has whitespace on the left side only, it is treated as a prefix unary operator. As an example, the ++ operator in a ++b is treated as a prefix unary operator.
* 如果运算符只有左侧空白，将被看作前缀一元运算符。例如 a ++b 中的 ++ 被看作前缀一元运算符。

* If an operator has whitespace on the right side only, it is treated as a postfix
unary operator. As an example, the ++ operator in a++ b is treated as a postfix unary operator.
* 如果运算符只有右侧空白，将被看作后缀一元运算符。例如 a++ b 中的 ++ 被看作后缀一元运算符。


* If an operator has no whitespace on the left but is followed immediately by a dot (.), it is treated as a postfix unary operator. As an example, the ++ operator in a++.b is treated as a postfix unary operator (a++ . b rather than a ++ .b).

* 如果运算符左侧没有空白并紧跟 .，将被看作后缀一元运算符。例如 a++.b 中的 ++ 被看作后缀一元运算符（同理， a++ . b 中的 ++ 是后缀一元运算符而 a ++ .b 中的 ++ 不是）.


For the purposes of these rules, the characters (, [, and { before an operator, the
characters ), ], and } after an operator, and the characters ,, ;, and : are also considered whitespace.

鉴于这些规则的目的，运算符前的字符 (、[ 和 { ；运算符后的字符 )、] 和 } 以及字符 ,、; 和: 同样被认为空白。

There is one caveat to the rules above. If the ! or ? operator has no whitespace on the left, it is treated as a postfix operator, regardless of whether it has whitespace on the right. To use the ? operator as syntactic sugar for the Optional type, it must not have whitespace on the left. To use it in the conditional (? :) operator, it must have whitespace around both sides.

以上规则有一点需要注意。如果运算符 ! 或 ? 左侧没有空白，则不管右侧是否有空白都将被看作后缀运算符。如果将 ? 用作修饰可选类型（optional type），左侧必须无空白。如果用于条件运算符 ? :，必须两侧都有空白。

In certain constructs, operators with a leading < or > may be split into two or more tokens. The remainder is treated the same way and may be split again. As a result, there is no need to use whitespace to disambiguate between the closing > characters in constructs like Dictionary<String, Array<Int>>. In this example, the closing > characters are not treated as a single token that may then be misinterpreted as a bit shift >> operator.

在特定构成中 ，以 < 或 > 开头的运算符会被分离成两个或多个标记，剩余部分以同样的方式会被再次分离。因此，在 Dictionary<String, Array<Int>> 中没有必要添加空白来消除闭合字符 > 的歧义。在这个例子中， 闭合字符 > 被看作单字符标记，而不会被误解为移位运算符 >>。

To learn how to define new, custom operators, see Custom Operators and Operator Declaration.To learn how to overload existing operators, see Operator Functions.

要学习如何自定义新的，自定义的运算符，请参考 自定义操作符 和 运算符声明。学习如何重写现有运算符，请参考 运算符方法。

> GRAMMAR OF OPERATORS

> 运算符语法语法
> 
> operator → operator-characteroperatoropt

> 运算符 → 运算符字符 运算符 可选

> operator-character → /  =  -  +  !  *  % <  >  &  |  ^  ~  .

> 运算符字符 → / | = | - | + | ! | * | % | < | > | & | | | ^ | ~ | .

> binary-operator → operator

> 二元运算符 → 运算符

> prefix-operator → operator

> 前置运算符 → 运算符

> postfix-operator → operator
> 后置运算符 → 运算符



