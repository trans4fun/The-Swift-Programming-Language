# Functions 函数

Functions are self-contained chunks of code that perform a specific task. You give a function a name that identifies what it does, and this name is used to “call” the function to perform its task when needed.

函数是执行特定任务的独立代码块。可以给函数起一个名字，标识它是做什么的，并在需要时使用这个名字来“调用”函数执行任务。

Swift’s unified function syntax is flexible enough to express anything from a simple C-style function with no parameter names to a complex Objective-C-style method with local and external parameter names for each parameter. Parameters can provide default values to simplify function calls and can be passed as in-out parameters, which modify a passed variable once the function has completed its execution.

Swift统一标准的函数语法十分灵活，可以表达任何函数。从简单的无参数名的C风格函数，到复杂的每个参数都带有局部和外部参数名的Objective-C风格函数。可以给参数提供默认值，以简化函数调用；也可以把参数当做in-out参数传值，函数执行结束时，可以改变传入变量的值。

Every function in Swift has a type, consisting of the function’s parameter types and return type. You can use this type like any other type in Swift, which makes it easy to pass functions as parameters to other functions, and to return functions from functions. Functions can also be written within other functions to encapsulate useful functionality within a nested function scope.

在Swift中，每个函数都有类型，由函数参数类型和返回类型组成。函数类型可以像任何其他类型那样使用，可以把函数作为参数传递给其他函数，也可以从函数中返回函数，函数类型让这些变得简单。函数也可以定义在另一个函数中， 在嵌套函数范围内，封装特定功能。


# Defining and Calling Functions 函数定义和调用

When you define a function, you can optionally define one or more named, typed values that the function takes as input (known as parameters), and/or a type of value that the function will pass back as output when it is done (known as its return type).

定义函数时，你可以定义一个或多个具有名称、类型的值作为函数输入（称为参数parameters），和（或者）定义在函数执行完毕后传回的一个有类型的值作为输出（称为返回值）。

Every function has a function name, which describes the task that the function performs. To use a function, you “call” that function with its name and pass it input values (known as arguments) that match the types of the function’s parameters. A function’s arguments must always be provided in the same order as the function’s parameter list.

每个函数都有一个函数名，用来描述此函数执行的任务。使用函数时，通过函数名“调用”函数，并传入符合函数参数类型的输入值（称为参数，arguments）。提供给函数的参数必须与函数参数列表的顺序一致。

The function in the example below is called greetingForPerson, because that’s what it does—it takes a person’s name as input and returns a greeting for that person. To accomplish this, you define one input parameter—a String value called personName—and a return type of String, which will contain a greeting for that person:

下面例子中的函数叫做sayHello，名字描述了它的用途，用人名作为输入，并返回对这个人的问候（greeting）。为了实现这些，需要定义一个输入参数——一个名为personName的String类型值，和一个带有对此人问候的String类型的返回值。

```js
func sayHello(personName: String) -> String {
    let greeting = "Hello, " + personName + "!"
    return greeting
}
```

All of this information is rolled up into the function’s definition, which is prefixed with the func keyword. You indicate the function’s return type with the return arrow -> (a hyphen followed by a right angle bracket), which is followed by the name of the type to return.

所有这些信息构成了一个函数的定义，并以关键字 func 作为前缀。使用返回箭头->（连字符后跟一个右尖括号）和紧接着的返回类型名来声明函数的返回类型。

The definition describes what the function does, what it expects to receive, and what it returns when it is done. The definition makes it easy for the function to be called elsewhere in your code in a clear and unambiguous way:

函数定义描述了函数是做什么的，期望接收什么和执行结束后返回什么。这个定义使得在代码中的任何地方可以清晰明确地调用函数变得简单。

```js
println(sayHello("Anna"))
// prints "Hello, Anna!"
println(sayHello("Brian"))
// prints "Hello, Brian!”
```

You call the sayHello function by passing it a String argument value in parentheses, such as sayHello("Anna"). Because the function returns a String value, sayHello can be wrapped in a call to the println function to print that string and see its return value, as shown above.

调用sayHello函数时，在圆括号中传入一个String类型参数值，例如sayHello(“Anna”)。由于这个函数返回了一个String类型的值，因此sayHello可以包装在 println 函数中，用来输出这个字符串并查看它的返回值，如上所示。

The body of the sayHello function starts by defining a new String constant called greeting and setting it to a simple greeting message for personName. This greeting is then passed back out of the function using the return keyword. As soon as return greeting is called, the function finishes its execution and returns the current value of greeting.

sayHello 的函数体先定义一个名为 greeting 的String 常量，并给它设置了对personName的简单问候信息。然后通过 return 关键字把 greeting 传出函数。一旦执行了 return greeting，函数就结束执行并返回greeting的当前值。

You can call the sayHello function multiple times with different input values. The example above shows what happens if it is called with an input value of "Anna", and an input value of "Brian". The function returns a tailored greeting in each case.

你可以传入不同的输入值多次调用sayHello 函数。上述例子展示了输入值为“Anna”和“Brian”时调用函数的结果。函数在每种情况下返回了各自定制的greeting。

To simplify the body of this function, combine the message creation and the return statement into one line:

为了简化函数体，可以把消息创建和返回语句合并为一行：

```js
func sayHelloAgain(personName: String) -> String {
    return "Hello again, " + personName + "!"
}
println(sayHelloAgain("Anna"))
// prints "Hello again, Anna!”
```

# Function Parameters and Return Values 函数参数和返回值


Function parameters and return values are extremely flexible in Swift. You can define anything from a simple utility function with a single unnamed parameter to a complex function with expressive parameter names and different parameter options.

Swift 中的函数参数和返回值十分灵活。你可以定义各种类型的函数，从只有一个未命名参数的简单功能函数到 具有表达性参数名和不同参数选项的复杂函数。

## Multiple Input Parameters 多输入参数

Functions can have multiple input parameters, which are written within the function’s parentheses, separated by commas.

函数可以有多个输入参数，写在函数的圆括号内，用逗号分隔。

This function takes a start and an end index for a half-open range, and works out how many elements the range contains:

下面这个函数接收半开区间的开始和结束索引，并计算出这个区间范围包含多少个元素：

```js
func halfOpenRangeLength(start: Int, end: Int) -> Int {
    return end - start
}
println(halfOpenRangeLength(1, 10))
// prints “9"
```

## Functions Without Parameters 无参数函数

Functions are not required to define input parameters. Here’s a function with no input parameters, which always returns the same String message whenever it is called:

函数可以不定义输入参数。下面是一个无输入参数的函数，不管何时调用总是返回相同的字符串信息：

```js
func sayHelloWorld() -> String {
    return "hello, world"
}
println(sayHelloWorld())
// prints "hello, world”
```

The function definition still needs parentheses after the function’s name, even though it does not take any parameters. The function name is also followed by an empty pair of parentheses when the function is called.

虽然定义这种函数，并不需要任何参数，但在函数名后仍需要一对括号。所以调用函数时，函数名后总是紧跟一对空括号。

## Functions Without Return Values 无返回值的函数

Functions are not required to define a return type. Here’s a version of the sayHello function, called waveGoodbye, which prints its own String value rather than returning it:

函数可以不定义返回类型。下面是sayHello 函数的另一个版本sayGoodbye，这个函数只输出String 值而不返回。
 
```js
func sayGoodbye(personName: String) {
    println("Goodbye, \(personName)!")
}
sayGoodbye("Dave")
// prints "Goodbye, Dave!”
```

Because it does not need to return a value, the function’s definition does not include the return arrow (->) or a return type.

由于这个函数不需要返回值，定义函数时不需要返回箭头（->）和返回类型。

> NOTE

> 注意

> Strictly speaking, the sayGoodbye function does still return a value, even though no return value is defined. Functions without a defined return type return a special value of type Void. This is simply an empty tuple, in effect a tuple with zero elements, which can be written as ().

> 严格来说，即使函数sayGoodbye没有定义返回值，它也会返回一个值。没有定义返回类型的函数会返回一个Void类型的特殊值。它仅仅是一个空元组（tuple），实际是零个元素的元组，可以写成()。

The return value of a function can be ignored when it is called:

调用函数时，函数的返回值可以忽略。

```js
func printAndCount(stringToPrint: String) -> Int {
    println(stringToPrint)
    return countElements(stringToPrint)
}
func printWithoutCounting(stringToPrint: String) {
    printAndCount(stringToPrint)
}
printAndCount("hello, world")
// prints "hello, world" and returns a value of 12
printWithoutCounting("hello, world")
// prints "hello, world" but does not return a value
```

The first function, printAndCount, prints a string, and then returns its character count as an Int. The second function, printWithoutCounting, calls the first function, but ignores its return value. When the second function is called, the message is still printed by the first function, but the returned value is not used.

第一个函数printAndCount 输出一个字符串并返回Int类型的字符个数。第二个函数 printWithoutCounting 调用第一个函数，但忽略它的返回值。调用第二个函数时，信息仍由第一个函数输出，但不使用它的返回值。

> NOTE

> 注意

> Return values can be ignored, but a function that says it will return a value must always do so. A function with a defined return type cannot allow control to fall out of the bottom of the function without returning a value, and attempting to do so will result in a compile-time error.

> 返回值虽然可以被忽略，但定义了返回类型的函数必须总是返回一个值。定义返回类型的函数不允许控制函数的最后没有返回值，试图这样做会导致编译时错误。

## Functions with Multiple Return Values 多返回值函数 

You can use a tuple type as the return type for a function to return multiple values as part of one compound return value.

可以使用元组类型作为函数的返回类型，这个函数可以返回多个值作为复合返回值的一部分。

The example below defines a function called count, which counts the number of vowels, consonants, and other characters in a string, based on the standard set of vowels and consonants used in American English:

下面的例子定义了count的函数，它基于美式英语中使用的元音和辅音的标准集合，来计算字符串中的元音、辅音和其他字符的个数：

```js
func count(string: String) -> (vowels: Int, consonants: Int, others: Int) {
    var vowels = 0, consonants = 0, others = 0
    for character in string {
        switch String(character).lowercaseString {
        case "a", "e", "i", "o", "u":
            ++vowels
        case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
        "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
            ++consonants
        default:
            ++others
        }
    }
    return (vowels, consonants, others)
}
```

You can use this count function to count the characters in an arbitrary string, and to retrieve the counted totals as a tuple of three named Int values:

你可以使用这个 count 函数来计算任意字符串中的字符数，然后得到所有字符总数——含有3个整型值的元组（译者注：元音，辅音，其他）。
 
```js
let total = count("some arbitrary string!")
println("\(total.vowels) vowels and \(total.consonants) consonants")
// prints "6 vowels and 13 consonants”
```

Note that the tuple’s members do not need to be named at the point that the tuple is returned from the function, because their names are already specified as part of the function’s return type.

注意当函数返回时，元组的成员不需要命名，因为它们的名字已经在函数返回类型中定义了，作为函数返回类型的一部分。

# Function Parameter Names 函数参数名

All of the above functions define parameter names for their parameters:

以上所有的函数都给它们的参数定义了参数名：

```js
func someFunction(parameterName: Int) {
    // function body goes here, and can use parameterName
    // to refer to the argument value for that parameter
}
```

However, these parameter names are only used within the body of the function itself, and cannot be used when calling the function. These kinds of parameter names are known as local parameter names, because they are only available for use within the function’s body.

然而，这些参数名只能在这个函数体内部使用，不能在调用函数时使用。这种参数名被称为局部参数名，因为它们只能在函数体内部获得和使用。

## External Parameter Names 外部参数名
 
Sometimes it’s useful to name each parameter when you call a function, to indicate the purpose of each argument you pass to the function.

有时，在调用函数时为每个参数命名十分有用，表明传给函数的每个参数的用途。

If you want users of your function to provide parameter names when they call your function, define an external parameter name for each parameter, in addition to the local parameter name. You write an external parameter name before the local parameter name it supports, separated by a space:

如果希望用户在调用函数时提供参数名，除了定义局部参数名，还要给每个参数定义外部参数名。把外部参数名写在支持的局部参数名前，用空格分隔：

```js
func someFunction(externalParameterName localParameterName: Int) {
    // function body goes here, and can use localParameterName
    // to refer to the argument value for that parameter
}
```

> NOTE 注意

> If you provide an external parameter name for a parameter, that external name must always be used when calling the function.

> 如果给参数提供了外部参数名，那么在调用函数时必须总是带上外部参数名。

As an example, consider the following function, which joins two strings by inserting a third “joiner” string between them:

例如下面的函数，把第三个名为“joiner”的字符串插入到另外两个字符串之间，进行字符串连接：

```js
func join(s1: String, s2: String, joiner: String) -> String {
    return s1 + joiner + s2
}
```

When you call this function, the purpose of the three strings that you pass to the function is unclear:

不过，在调用这个函数时，传给函数的三个字符串的用意并不明确：

```js
join("hello", "world", ", ")
// returns "hello, world”
```

To make the purpose of these String values clearer, define external parameter names for each join function parameter:

为了明确这些字符串值的用途，需要给 join 函数的每个参数定义外部参数名：

```
func join(string s1: String, toString s2: String, withJoiner joiner: String)
    -> String {
        return s1 + joiner + s2
}
```

In this version of the join function, the first parameter has an external name of string and a local name of s1; the second parameter has an external name of toString and a local name of s2; and the third parameter has an external name of withJoiner and a local name of joiner.

在这个版本的 join 函数中，第一个参数具有外部参数名 string 和 局部参数名 s1；第二个参数具有外部参数名 toString 和 局部参数名 s2；第三个参数具有外部参数名 withJoiner 和 局部参数名 joiner；

You can now use these external parameter names to call the function in a clear and unambiguous way:

现在你就可以明确清楚地使用这些外部参数名来调用函数：

```js
join(string: "hello", toString: "world", withJoiner: ", ")
// returns "hello, world”
```

The use of external parameter names enables this second version of the join function to be called in an expressive, sentence-like manner by users of the function, while still providing a function body that is readable and clear in intent.

利用外部参数使调用第二个版本的join函数更具表达性和语义性，同时也使函数体更可读、更清晰。

> NOTE 注意

> Consider using external parameter names whenever the purpose of a function’s arguments would be unclear to someone reading your code for the first time. You do not need to specify external parameter names if the purpose of each parameter is clear and unambiguous when the function is called.

> 初次阅读这些代码的人，可能不清楚函数参数的用途，这时需要考虑使用外部参数名。如果调用函数时，每个参数的用意都很清楚、明确，那就不需要定义外部参数名。

## Shorthand External Parameter Names 简写外部参数名

If you want to provide an external parameter name for a function parameter, and the local parameter name is already an appropriate name to use, you do not need to write the same name twice for that parameter. Instead, write the name once, and prefix the name with a hash symbol (#). This tells Swift to use that name as both the local parameter name and the external parameter name.

如果想给函数参数提供外部参数名，而局部参数名已经很适合了，那么你不需要给参数写两个相同的名字。而只用写一次，然后在名字前加上符号(#)。这就告诉Swift使用这个名字同时作为本地参数名和外部参数名。

This example defines a function called containsCharacter, which defines external parameter names for both of its parameters by placing a hash symbol before their local parameter names:

下面的例子定义了containsCharacter的函数，这个函数在局部参数名前加上#标识从而给它的两个参数定义外部参数名。
 
```js
func containsCharacter(#string: String, #characterToFind: Character) -> Bool {
    for character in string {
        if character == characterToFind {
            return true
        }
    }
    return false
}
```

This function’s choice of parameter names makes for a clear, readable function body, while also enabling the function to be called without ambiguity:

这个函数选择的参数名使函数体清晰、可读，同时在调用函数时也没有歧义：

```js
let containsAVee = containsCharacter(string: "aardvark", characterToFind: "v")
// containsAVee equals true, because "aardvark" contains a “v"
```

## Default Parameter Values 默认参数值

You can define a default value for any parameter as part of a function’s definition. If a default value is defined, you can omit that parameter when calling the function.

在函数定义中，你可以给任何参数定义默认值。如果定义了默认值，在调用函数时可以忽略这个参数。

> NOTE 注意

> Place parameters with default values at the end of a function’s parameter list. This ensures that all calls to the function use the same order for their non-default arguments, and makes it clear that the same function is being called in each case.

> 把带有默认值的参数放在函数参数列表的最后。这样可以确保，所有的函数调用使用的非默认参数顺序相同，同时可以明确每种情况都会调用相同的函数。

Here’s a version of the join function from earlier, which provides a default value for its joiner parameter:

下面是之前版本的 join 函数，这个函数为它的joiner 参数提供了默认值：

```js
func join(string s1: String, toString s2: String,
    withJoiner joiner: String = " ") -> String {
        return s1 + joiner + s2
}
```

If a string value for joiner is provided when the join function is called, that string value is used to join the two strings together, as before:

调用 join 函数时，如果给 joiner 提供了字符串类型的值，这个字符串值会像之前一样，连接 另外两个字符串：

```js
join(string: "hello", toString: "world", withJoiner: "-")
// returns "hello-world”
```

However, if no value of joiner is provided when the function is called, the default value of a single space (" ") is used instead:

然而，如果调用函数时没有提供 joiner 值，会使用默认值空格（“ ”）替代：

```js
join(string: "hello", toString: "world")
// returns "hello world”
```

## External Names for Parameters with Default Values 带默认值参数的外部参数名

In most cases, it is useful to provide (and therefore require) an external name for any parameter with a default value. This ensures that the argument for that parameter is clear in purpose if a value is provided when the function is called.

在大多数情况下，给任何带有默认值的参数提供外部参数名十分有用(而且非常必要)。这可以确保在给函数调用提供值时，参数的用途是明确的。

To make this process easier, Swift provides an automatic external name for any defaulted parameter you define, if you do not provide an external name yourself. The automatic external name is the same as the local name, as if you had written a hash symbol before the local name in your code.

为了使定义外部参数名更简单，如果你没有提供自定义的外部参数名，Swift 会为你定义的任何默认参数自动提供外部参数名。在代码中，如果你已经在本地参数名前加上 # 标识，那么自动外部参数名和本地参数名相同。

Here’s a version of the join function from earlier, which does not provide external names for any of its parameters, but still provides a default value for its joiner parameter:

下面是 join函数之前的版本，这个函数没有给它的任何参数提供外部参数名，但仍然为它的 joiner 参数提供了默认值。

```js
func join(s1: String, s2: String, joiner: String = " ") -> String {
    return s1 + joiner + s2
}
```

In this case, Swift automatically provides an external parameter name of joiner for the defaulted parameter. The external name must therefore be provided when calling the function, making the parameter’s purpose clear and unambiguous:

在这个例子中，Swift自动为默认参数joiner提供了外部参数名。因此，在调用该函数时，必须使用外部参数名，使这个参数的用途明确清晰。

```js
join("hello", "world", joiner: "-")
// returns "hello-world”
```

> NOTE 注意

> You can opt out of this behavior by writing an underscore (_) instead of an explicit external name when you define the parameter. However, external names for defaulted parameters are always preferred where appropriate.

> 定义参数时，可以使用下划线（_）来避免显式使用参数外部名。不过，在大多情况下，都推荐为有默认值的参数提供外部参数名。

## Parameters 可变参数

A variadic parameter accepts zero or more values of a specified type. You use a variadic parameter to specify that the parameter can be passed a varying number of input values when the function is called. Write variadic parameters by inserting three period characters (...) after the parameter’s type name.

可变参数接收指定类型的零个或多个值。调用函数时，参数可以传入不定个数的输入值。这种参数定义为可变参数。通过在参数类型名后插入3个点字符（…）来定义可变参数。

The values passed to a variadic parameter are made available within the function’s body as an array of the appropriate type. For example, a variadic parameter with a name of numbers and a type of Double... is made available within the function’s body as a constant array called numbers of type Double[].

传给可变参数的值，在函数体内部可以当做相应类型的数组使用。例如，名为 numbers 的 Double...类型的可变参数，可以在函数体内部作为名为numbers的Double[]类型的常量数组使用。

The example below calculates the arithmetic mean (also known as the average) for a list of numbers of any length:

下面的例子可以对一个有任意个数的数字列表求算术平均数（也被称为平均数）

```js
func arithmeticMean(numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)
// returns 3.0, which is the arithmetic mean of these five numbers
arithmeticMean(3, 8, 19)
// returns 10.0, which is the arithmetic mean of these three numbers
```

> NOTE 注意 

> A function may have at most one variadic parameter, and it must always appear last in the parameter list, to avoid ambiguity when calling the function with multiple parameters.

> 在调用带有多个参数的函数时，为了避免产生歧义，函数最多只能有一个可变参数，而且它必须总是放在参数列表的最后。


> If your function has one or more parameters with a default value, and also has a variadic parameter, place the variadic parameter after all the defaulted parameters at the very end of the list.

> 如果函数有一个或多个参数带有默认值，且还有一个可变参数，请把可变参数放在所有默认参数列表的最后。

## Constant and Variable Parameters 常量参数和变量参数

Function parameters are constants by default. Trying to change the value of a function parameter from within the body of that function results in a compile-time error. This means that you can’t change the value of a parameter by mistake.

函数参数默认都是常量。试图在函数体内改变参数值会导致编译时错误。这会防止你意外地改变参数值。

However, sometimes it is useful for a function to have a variable copy of a parameter’s value to work with. You can avoid defining a new variable yourself within the function by specifying one or more parameters as variable parameters instead. Variable parameters are available as variables rather than as constants, and give a new modifiable copy of the parameter’s value for your function to work with.

然而，有时使用参数的拷贝值对于函数来说十分有用。为了避免在函数内部定义新变量，可以把一个或多个参数定义为变量参数。这时，变量参数可以作为变量而不是常量使用，并且提供一个新的可修改的参数值的拷贝给函数使用。

Define variable parameters by prefixing the parameter name with the keyword var:

可以在参数名前增加关键字 var 来定义变量参数：

```js
func alignRight(var string: String, count: Int, pad: Character) -> String {
    let amountToPad = count - countElements(string)
    for _ in 1...amountToPad {
        string = pad + string
    }
    return string
}
let originalString = "hello"
let paddedString = alignRight(originalString, 10, "-")
// paddedString is equal to "-----hello"
// originalString is still equal to “hello"
```

This example defines a new function called alignRight, which aligns an input string to the right edge of a longer output string. Any space on the left is filled with a specified padding character. In this example, the string "hello" is converted to the string "-----hello”.

这个例子定义了名为alignRight的新函数，它把输入的字符串放在一个更长的输出字符串的最右端（译者注：以实现右对齐）。这个字符串的左边用指定的字符填充。在这个例子中，字符串“hello” 转换为 字符串“——hello”。

The alignRight function defines the input parameter string to be a variable parameter. This means that string is now available as a local variable, initialized with the passed-in string value, and can be manipulated within the body of the function.

函数alignRight 把输入参数 string 定义为变量参数。这意味着在函数体内部可以把string当做局部变量使用，并初始化为传入的字符串值。

The function starts by working out how many characters need to be added to the left of string in order to right-align it within the overall string. This value is stored in a local constant called amountToPad. The function then adds amountToPad copies of the pad character to the left of the existing string and returns the result. It uses the string variable parameter for all its string manipulation.

为了在整个字符串中右对齐 string，首先要算出 string 的左边需要添加多少字符。这个值储存在局部常量 amoutToPad 中。然后，函数在现有 string 的左边添加 amoutToPad 多个填充字符并返回结果。所有对 string 的操作均使用了 string 的可变参数。

> NOTE 

> The changes you make to a variable parameter do not persist beyond the end of each call to the function, and are not visible outside the function’s body. The variable parameter only exists for the lifetime of that function call.

> 变量参数的改变可以持续到每个函数调用的结束（不会超过），并在函数体外不可见。变量参数只存在于函数调用的生命周期中。

## In-Out Parameters In-Out参数

Variable parameters, as described above, can only be changed within the function itself. If you want a function to modify a parameter’s value, and you want those changes to persist after the function call has ended, define that parameter as an in-out parameter instead.

变量参数，如前所述，只能在函数自身内部改变。如果希望函数可以修改参数值，并且这些变化持续到函数调用结束之后，需要定义该参数为In-Out 参数。

You write an in-out parameter by placing the inout keyword at the start of its parameter definition. An in-out parameter has a value that is passed in to the function, is modified by the function, and is passed back out of the function to replace the original value.

在定义的参数前添加inout关键字，可以定义in-out参数。传给函数的in-out参数的值会被函数修改，然后被传出函数，替换原来的值。

You can only pass a variable as the argument for an in-out parameter. You cannot pass a constant or a literal value as the argument, because constants and literals cannot be modified. You place an ampersand (&) directly before a variable’s name when you pass it as an argument to an inout parameter, to indicate that it can be modified by the function.

in-out参数作为函数参数，只能传入变量，不能传入常量或字面量。因为常量和字面量不能被修改。在变量名前直接加上&，把它作为参数传给inout参数，表示它可以被函数修改。

> NOTE 注意 

> In-out parameters cannot have default values, and variadic parameters cannot be marked as inout. If you mark a parameter as inout, it cannot also be marked as var or let.

> In-out参数不能有默认值，且可变参数不能用inout标记。如果定义一个参数为inout参数，就不能再用var或let标记。

Here’s an example of a function called swapTwoInts, which has two in-out integer parameters called a and b:

下面是swapTwoInts函数的例子，它有两个inout 整型参数a和b：

```js
func swapTwoInts(inout a: Int, inout b: Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

The swapTwoInts function simply swaps the value of b into a, and the value of a into b. The function performs this swap by storing the value of a in a temporary constant called temporaryA, assigning the value of b to a, and then assigning temporaryA to b.

函数swapTwoInts简单地交换a、b值。先把a值存储在临时常量temporaryA中，然后把b值赋给a，最后把temporaryA赋值给b来实现交换。

You can call the swapTwoInts function with two variables of type Int to swap their values. Note that the names of someInt and anotherInt are prefixed with an ampersand when they are passed to the swapTwoInts function:

可以调用 swapTwoInts 函数交换两个 Int 型变量的值。注意把someInt 和anotherInt 传给swapTwoInts函数时，它们的名字前都有&作为前缀：

```js
var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
println("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
// prints "someInt is now 107, and anotherInt is now 3”
```

The example above shows that the original values of someInt and anotherInt are modified by the swapTwoInts function, even though they were originally defined outside of the function.

上面的例子显示出函数 swapTwoInts 改变了 someInt 和anotherInt 的初始值，尽管它们的初始值是在函数外定义的。

> NOTE 注意

> In-out parameters are not the same as returning a value from a function. The swapTwoInts example above does not define a return type or return a value, but it still modifies the values of someInt and anotherInt. In-out parameters are an alternative way for a function to have an effect outside of the scope of its function body.

> In-out参数和函数返回值不一样。虽然上面swapTwoInts的例子没有定义返回类型和返回值，但它仍然修改了someInt 和anotherInt的值。In-out参数是函数对函数体范围外产生影响的另一种方式。

# Function Types 函数类型

Every function has a specific function type, made up of the parameter types and the return type of the function.

每个函数都有一个特定的函数类型，由函数参数类型和返回类型组成。

For example:

例如：

```js
func addTwoInts(a: Int, b: Int) -> Int {
    return a + b
}
func multiplyTwoInts(a: Int, b: Int) -> Int {
    return a * b
}
```

This example defines two simple mathematical functions called addTwoInts and multiplyTwoInts. These functions each take two Int values, and return an Int value, which is the result of performing an appropriate mathematical operation.

这个例子定义了两个简单的数学函数addTwoInts和multiplyTwoInts。每个函数都接受两个整型值并返回一个整型值——执行相应数学运算的结果。

The type of both of these functions is (Int, Int) -> Int. This can be read as:

这两个函数的类型都是(Int, Int) -> Int，可以解读为：

“A function type that has two parameters, both of type Int, and that returns a value of type Int.”

这个函数类型有两个Int类型参数和一个Int类型返回值。

Here’s another example, for a function with no parameters or return value:

下面是另一个例子，没有参数和返回值的函数。

```js
func printHelloWorld() {
    println("hello, world")
}
```

The type of this function is () -> (), or “a function that has no parameters, and returns Void.” Functions that don’t specify a return value always return Void, which is equivalent to an empty tuple in Swift, shown as ().

这个函数的类型是() -> ()，或理解为”没有参数，且返回Void的函数。“不定义返回值的函数始终返回Void，相当于Swift中的空元组，写作()。

## Using Function Types 函数类型的使用

You use function types just like any other types in Swift. For example, you can define a constant or variable to be of a function type and assign an appropriate function to that variable:

你可以像使用Swift中任何其他类型那样使用函数类型。例如，可以定义一个函数类型的常量或变量，并且把对应的函数赋值给它。

```js
var mathFunction: (Int, Int) -> Int = addTwoInts
```

This can be read as:

这可以解读为：

“Define a variable called mathFunction, which has a type of ‘a function that takes two Int values, and returns an Int value.’ Set this new variable to refer to the function called addTwoInts.”

”定义名为mathFunction的变量，该变量类型为’可以接收两个Int类型参数并返回Int类型值的函数’。设置这个新变量指向addTwoInts函数“

The addTwoInts function has the same type as the mathFunction variable, and so this assignment is allowed by Swift’s type-checker.

函数addTwoInts 和mathFunction 有相同的类型，因此Swift的类型检查允许这种赋值。

You can now call the assigned function with the name mathFunction:

可以使用mathFunction名来调用被赋值的函数：

```js
println("Result: \(mathFunction(2, 3))")
// prints "Result: 5”
```

A different function with the same matching type can be assigned to the same variable, in the same way as for non-function types:

可以把具有相同类型的不同函数赋值给同一变量，对于无函数类型的函数也适用。

```js
mathFunction = multiplyTwoInts
println("Result: \(mathFunction(2, 3))")
// prints "Result: 6”
```
As with any other type, you can leave it to Swift to infer the function type when you assign a function to a constant or variable:

与其他类型一样，当把函数赋值给常量或变量时，可以留给Swift来推断函数类型。

```js
let anotherMathFunction = addTwoInts
// anotherMathFunction is inferred to be of type (Int, Int) -> Int
```

## Function Types as Parameter Types 作为参数类型的函数类型

You can use a function type such as (Int, Int) -> Int as a parameter type for another function. This enables you to leave some aspects of a function’s implementation for the function’s caller to provide when the function is called.

可以使用类似 (Int, Int) -> Int的函数类型作为另一个函数的参数类型。这样在函数调用时，可以把一个函数的某些实现留给函数调用者。

Here’s an example to print the results of the math functions from above:

下面的例子可以输出上面数学函数的计算结果。

```js
func printMathResult(mathFunction: (Int, Int) -> Int, a: Int, b: Int) {
    println("Result: \(mathFunction(a, b))")
}
printMathResult(addTwoInts, 3, 5)
// prints "Result: 8”
```

This example defines a function called printMathResult, which has three parameters. The first parameter is called mathFunction, and is of type (Int, Int) -> Int. You can pass any function of that type as the argument for this first parameter. The second and third parameters are called a and b, and are both of type Int. These are used as the two input values for the provided math function.

这个例子定义了printMathResult函数，它有三个参数。第一参数是 mathFunction，(Int, Int) -> Int类型的。可以传入任何这种类型的函数作为该函数的第一个参数。第二和第三个参数是a和b，都是Int类型。把它们作为所提供的数学函数的两个输入值。

When printMathResult is called, it is passed the addTwoInts function, and the integer values 3 and 5. It calls the provided function with the values 3 and 5, and prints the result of 8.

调用printMathResult 时，传入addTwoInts 函数、Int类型的3和5作为参数。让后把3和5作为参数调用 addTwoInts ，最后输出结果8。

The role of printMathResult is to print the result of a call to a math function of an appropriate type. It doesn’t matter what that function’s implementation actually does—it matters only that the function is of the correct type. This enables printMathResult to hand off some of its functionality to the caller of the function in a type-safe way.

函数printMathResult 的作用是输出相应类型的数学函数的调用结果。它与传入函数的具体实现无关，只与函数具有的正确类型有关。这让函数 printMathResult 以类型安全的方式，把它的部分功能交给其调用者去实现。

## Function Types as Return Types

## 作为返回类型的函数类型

You can use a function type as the return type of another function. You do this by writing a complete function type immediately after the return arrow (->) of the returning function.

可以使用函数 类型作为另一个函数的返回类型。需要在返回函数的返回箭头（->）后编写完整的函数类型。 

The next example defines two simple functions called stepForward and stepBackward. The stepForward function returns a value one more than its input value, and the stepBackward function returns a value one less than its input value. Both functions have a type of (Int) -> Int:

下面的例子定义了stepForward 和stepBackward两个简单函数。stepForward 函数返回值比输入值多1，而stepBackward 函数返回值比输入值少1.这两个函数都是 (Int) -> Int类型：

```js
func stepForward(input: Int) -> Int {
    return input + 1
}
func stepBackward(input: Int) -> Int {
    return input - 1
}
```

Here’s a function called chooseStepFunction, whose return type is “a function of type (Int) -> Int”. chooseStepFunction returns the stepForward function or the stepBackward function based on a Boolean parameter called backwards:

下面是函数chooseStepFunction，它的返回类型是(Int) -> Int的函数。chooseStepFunction 根据Boolean 类型参数 backwards 判断是返回 stepForward 函数，还是返回 stepBackward 函数。

```js
func chooseStepFunction(backwards: Bool) -> (Int) -> Int {
    return backwards ? stepBackward : stepForward
}
```

You can now use chooseStepFunction to obtain a function that will step in one direction or the other:

使用函数chooseStepFunction，可以获得返回函数，指示前进或后退。

```js
var currentValue = 3
let moveNearerToZero = chooseStepFunction(currentValue > 0)
// moveNearerToZero now refers to the stepBackward() function
```

The preceding example works out whether a positive or negative step is needed to move a variable called currentValue progressively closer to zero. currentValue has an initial value of 3, which means that currentValue > 0 returns true, causing chooseStepFunction to return the stepBackward function. A reference to the returned function is stored in a constant called moveNearerToZero.

前面的例子实现了是需要正向还是反向移动，使得变量 currentValue 逐步趋向于零的功能。currentValue 的初始值是3，这意味着currentValue > 0 返回true，使得chooseStepFunction 返回stepBackward 函数。返回的函数引用存储在常量moveNearerToZero中。


Now that moveNearerToZero refers to the correct function, it can be used to count to zero:

现在 moveNearerToZero 指向了正确的函数，可以用来计数到零：

```js
println("Counting to zero:")
// Counting to zero:
while currentValue != 0 {
    println("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
println("zero!")
// 3...
// 2...
// 1...
// zero!
```

# Nested Functions
# 嵌套函数

All of the functions you have encountered so far in this chapter have been examples of global functions, which are defined at a global scope. You can also define functions inside the bodies of other functions, known as nested functions.

到目前为止，本章所有的全局函数都是在全局范围定义的。也可以在其他函数的内部定义函数，称为嵌套函数。

Nested functions are hidden from the outside world by default, but can still be called and used by their enclosing function. An enclosing function can also return one of its nested functions to allow the nested function to be used in another scope.

默认情况下，嵌套函数不能在外部访问，但仍可以被闭包函数调用。闭包函数也可以返回它其中一个嵌套函数，使得这个嵌套函数可以在其他作用域内使用。

You can rewrite the chooseStepFunction example above to use and return nested functions:

可以重写上面的chooseStepFunction 例子来返回嵌套函数：

```js
func chooseStepFunction(backwards: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    return backwards ? stepBackward : stepForward
}
var currentValue = -4
let moveNearerToZero = chooseStepFunction(currentValue > 0)
// moveNearerToZero now refers to the nested stepForward() function
while currentValue != 0 {
    println("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
println("zero!")
// -4...
// -3...
// -2...
// -1...
// zero!
```
