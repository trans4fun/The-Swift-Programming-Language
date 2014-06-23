# Closures 闭包

Closures are self-contained blocks of functionality that can be passed around and used in your code. Closures in Swift are similar to blocks in C and Objective-C and to lambdas in other programming languages.

闭包是一个封闭的代码块，可以在你的程序中传递和使用。swift中的闭包跟objective-C和C语言中的block很类似，其他语言中的匿名函数也跟此相似。

Closures can capture and store references to any constants and variables from the context in which they are defined. This is known as closing over those constants and variables, hence the name “closures”. Swift handles all of the memory management of capturing for you.

闭包可以将常量和变量从定义的地方通过捕获和指针引用保存起来，可以理解成将这些常量和变量封闭了起来，所以取名为“闭包”。swift会帮你处理所有闭包涉及的内存管理。

> note：
> Don’t worry if you are not familiar with the concept of “capturing”. It is explained in detail below in Capturing Values.
> 如果你还不是很熟悉“capturing”，这里有关于“capturing values”的细节。

Global and nested functions, as introduced in Functions, are actually special cases of closures. Closures take one of three forms:

前面介绍过的全局函数和嵌套函数其实是闭包的特殊情况，闭包有以下三种：

* Global functions are closures that have a name and do not capture any values.
* 全局函数是一种拥有函数名但是不会捕获任何值的闭包

* Nested functions are closures that have a name and can capture values from their enclosing function.
* 嵌套的函数是一种拥有函数名并且会捕获变量和常量得闭包

* Closure expressions are unnamed closures written in a lightweight syntax that can capture values from their surrounding context.
* 闭包表达式是一种没有名字的闭包，他通过轻量简便的语法定义，可以从他们的上下文中捕获变量和常量

Swift’s closure expressions have a clean, clear style, with optimizations that encourage brief, clutter-free syntax in common scenarios. These optimizations include:

swift中的闭包表达式是一种非常简洁明了的语法，通过使用优化的闭包语法，使的一般场景中的代码显得非常的整洁，这些优化包含

* Inferring parameter and return value types from context
* 从上下文中自动推断出返回值类型

* Implicit returns from single-expression closures
* 单条语句的闭包自动获得隐式的返回

* Shorthand argument names
* 简化的参数名称(通过使用$0...$n来使用参数)

* Trailing closure syntax
* 返回类型后置语法（函数返回值类型位于函数声明的末端）

## Closure Expressions 闭包表达式

Nested functions, as introduced in Nested Functions, are a convenient means of naming and defining self-contained blocks of code as part of a larger function. However, it is sometimes useful to write shorter versions of function-like constructs without a full declaration and name. This is particularly true when you work with functions that take other functions as one or more of their arguments.

嵌套的函数是一种自我包含的代码块，这是一种简单方便的方式,尤其在更大的函数中使用的时候。但是有时候通过一种更简洁的方式来定义函数会显得很实用，尤其在一些函数使用其他函数作为参数的时候。

Closure expressions are a way to write inline closures in a brief, focused syntax. Closure expressions provide several syntax optimizations for writing closures in their simplest form without loss of clarity or intent. The closure expression examples below illustrate these optimizations by refining a single example of the sort function over several iterations, each of which expresses the same functionality in a more succinct way.

     闭包表达式是一种简洁并且聚焦的方式来定义内联的闭包，闭包表达式提供几种优化过的语法来定义闭包，并且不会看起来有混淆和歧义。下面的闭包表达式例子定义一些简单的排序函数，每一种都通过更简洁明了的方式达到了同样的目的。
     

### The Sort Function 排序函数

Swift’s standard library provides a function called sort, which sorts an array of values of a known type, based on the output of a sorting closure that you provide. Once it completes the sorting process, the sort function returns a new array of the same type and size as the old one, with its elements in the correct sorted order.

     swift的标准库提供了一个函数叫做sort，通过你提供的排序闭包用来对数组中的元素进行排序。一旦完成排序，sort函数会返回一个跟以前类型和数量一样的数组，并且里面的元素都已经排列成正确的顺序。

The closure expression examples below use the sort function to sort an array of String values in reverse alphabetical order. Here’s the initial array to be sorted:

     下面的闭包表达式例子通过使用sort函数来对一个都是string类型的数组排序，数组的定义如下

```js
     let names = ["Chris","Alex","Ewa","Barry","Daniella"]
```

The sort function takes two arguments:

sort函数有2个参数

* An array of values of a known type.
* A closure that takes two arguments of the same type as the array’s contents, and returns a Bool value to say whether the first value should appear before or after the second value once the values are sorted. The sorting closure needs to return true if the first value should appear before the second value, and false otherwise.

This example is sorting an array of String values, and so the sorting closure needs to be a function of type (String, String) -> Bool.

这是一个对string类型的数组进行排序的例子，所以这个排序的闭包需要有以下类型(String,String) ->Bool.

One way to provide the sorting closure is to write a normal function of the correct type, and to pass it in as the sort function’s second parameter:

函数名字加正确的类型是排序闭包的写法之一，然后在sort函数中作为第二个参数传入。

```js
func backwards(s1:String,s2:String) -> Bool{
  return s1>s2
}

var reversed = sort(names,backwards)
// reversed is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
```

If the first string (s1) is greater than the second string (s2), the backwards function will return true, indicating that s1 should appear before s2 in the sorted array. For characters in strings, “greater than” means “appears later in the alphabet than”. This means that the letter "B" is “greater than” the letter "A", and the string "Tom" is greater than the string "Tim". This gives a reverse alphabetical sort, with "Barry" being placed before "Alex", and so on.

如果第一个字符串s1比第二个字符串s2比较值更大，函数backwards会返回true，这样在排序之后的数组中s1应该会排在s2之前，对于在字符串中的字符来说，“值大于”等于“在字符表中出现的更晚”，这意味着字符”B“比字符”A“的值更大，所以字符串”Tom“会比”Tim“更大。这个排序将会把字符表倒序排列，所以”Barry“会放在”Alex"之前。

However, this is a rather long-winded way to write what is essentially a single-expression function (a > b). In this example, it would be preferable to write the sorting closure inline, using closure expression syntax.

然而这么繁重的写法在本质上只是一个表达式：a>b.在下面的例子里，使用闭包表达式写排序内联的闭包将会是更好的方式

### Closure Expression Syntax 闭包表达式语法

Closure expression syntax has the following general form:

比表表达式语法定义如下：

{ (parameters) -> return type in
    statements
}

{(参数）-> 返回值 in 
    语句
}

Closure expression syntax can use constant parameters, variable parameters, and inout parameters. Default values cannot be provided. Variadic parameters can be used if you name the variadic parameter and place it last in the parameter list. Tuples can also be used as parameter types and return types.

闭包表达式语法可以使用常量，变量还有inout来作为参数，不能提供缺省参数，如果你要使用可选参数可以将它们定义在参数列表的结尾，tuples可以作为参数和返回值类型。

The example below shows a closure expression version of the backwards function from earlier:

下面的例子是闭包表达式版本的backwords排序函数：

```js
reversed = sort(names,{(s1:String,s2:String) -> Bool in 
return s1>s2})
```

Note that the declaration of parameters and return type for this inline closure is identical to the declaration from the backwards function. In both cases, it is written as (s1: String, s2: String) -> Bool. However, for the inline closure expression, the parameters and return type are written inside the curly braces, not outside of them.

在这个表达式的定义和返回值类型跟前面的backwords函数完全相同，在这两个例子中，都是这样写的（s1:String,s2:String)->Bool,然而对于内联的闭包表达式，参数和返回值类型都写在大括号里面。

The start of the closure’s body is introduced by the in keyword. This keyword indicates that the definition of the closure’s parameters and return type has finished, and the body of the closure is about to begin.

闭包语句的书写在关键字in之后，这个关键字表明的意思是：闭包表达式的参数和返回值类型已经定义结束，闭包的语句可以开始书写了。
Because the body of the closure is so short, it can even be written on a single line:

因为这个闭包的语句太短了，所以可以写在一行之内

```js
reversed = sort(name,{(s1:String,s2:String) -> Bool in return s1 > s2 })
```

This illustrates that the overall call to the sort function has remained the same. A pair of parentheses still wrap the entire set of arguments for the function. However, one of those arguments is now an inline closure.

这个表达式在sort函数中跟前面的例子得到的效果是完全一样的，一对圆括号包含了函数中所有的参数集。

### Inferring Type From Context 上下文推断返回值类型

Because the sorting closure is passed as an argument to a function, Swift can infer the types of its parameters and the type of the value it returns from the type of the sort function’s second parameter. This parameter is expecting a function of type (String, String) -> Bool. This means that the String, String, and Bool types do not need to be written as part of the closure expression’s definition. Because all of the types can be inferred, the return arrow (->) and the parentheses around the names of the parameters can also be omitted:

由于排序的闭包是作为函数的参数传入的，swift会根据sort函数的第二的参数类型来推断其参数参数和返回值的类型。这个参数期望的函数类型为(String,String)->Bool,这意味着String,String和BOOL类型并不强制需要在写闭包表达式里，因为所有类型都可以推断，返回的箭头->和他周围的参数名字都可以被省略

```js
     reversed = sort(names,{s1,s2 in return s1 > s2)})
```

It is always possible to infer parameter types and return type when passing a closure to a function as an inline closure expression. As a result, you rarely need to write an inline closure in its fullest form.

作为函数参数的内联闭包表达式都可以推断参数和返回值的类型，所以你很少需要写内联闭包的完整形式。

Nonetheless, you can make the types explicit if you wish, and doing so is encouraged if it avoids ambiguity for readers of your code. In the case of the sort function, the purpose of the closure is clear from the fact that sorting is taking place, and it is safe for a reader to assume that the closure is likely to be working with String values, because it is assisting with the sorting of an array of strings.

虽然如此，如果你愿意你可以明确的写出参数的类型，这样可以让你的代码阅读起来能减少歧义。

### Implicit Returns from Single-Expression Closures 单表达式的隐式返回值

Single-expression closures can implicitly return the result of their single expression by omitting the return keyword from their declaration, as in this version of the previous example:

     单表达式的返回值可以通过隐藏return关键字来隐式返回结果，上面的表达式可以写成：

```js
     reversed = sort（names,{s1,s2 in s1 > s2})
```

Here, the function type of the sort function’s second argument makes it clear that a Bool value must be returned by the closure. Because the closure’s body contains a single expression (s1 > s2) that returns a Bool value, there is no ambiguity, and the return keyword can be omitted.

    这个例子里面，sort的第二个参数类型定义了闭包的返回值是BOOL类型，而且闭包表达式中只包含了一个表达式 （s1 >s2）而且这个表达式返回BOOL类型，所以这里省略掉return没有歧义。

### Shorthand Argument Names 参数名的缩写

Swift automatically provides shorthand argument names to inline closures, which can be used to refer to the values of the closure’s arguments by the names $0, $1, $2, and so on.

swift里为内联的参数提供了参数的缩写功能，你可以通过$0,$1,$2来调用闭包的参数。

If you use these shorthand argument names within your closure expression, you can omit the closure’s argument list from its definition, and the number and type of the shorthand argument names will be inferred from the expected function type. The in keyword can also be omitted, because the closure expression is made up entirely of its body:

如果你在闭包表达式中使用参数名称的缩写，在闭包参数列表中就可以省略对其的定义，对应参数的类型将会通过函数参数的定义来推断，in关键字也可以被忽略掉：

```js
     reversed = sort(name,{$0>$1} )
```

Here, $0 and $1 refer to the closure’s first and second String arguments.

 这个例子中，$0和$1表示闭包中的第一和第二个参数

### Operator Functions 运算符函数

There’s actually an even shorter way to write the closure expression above. Swift’s String type defines its string-specific implementation of the greater-than operator (>) as a function that has two parameters of type String, and returns a value of type Bool. This exactly matches the function type needed for the sort function’s second parameter. Therefore, you can simply pass in the greater-than operator, and Swift will infer that you want to use its string-specific implementation:

实际上还有更精简的方式来书写上面的闭包表达式，swift的String类型对于大于号(>)做了特别的实现，作为函数接受两个String类型的参数，返回值是BOOL类型,刚好满足sort函数中第二个参数的函数类型定义，所以，你可以简单的将大于运算法传递进去，swift会推断你需要使用这个String的运算符函数

```js
     reversed = sort(names,>)
```

For more about operator functions, see Operator Functions.

更多关于运算符函数请看 Operator Functions

## Trailing Closures 跟尾闭包

If you need to pass a closure expression to a function as the function’s final argument and the closure expression is long, it can be useful to write it as a trailing closure instead. A trailing closure is a closure expression that is written outside of (and after) the parentheses of the function call it supports:

如果你需要将一个闭包表达式作为一个函数的最后一个参数传入，使用跟尾闭包的写法会更有可读性，尾闭包表达式全部写在函数最后的括号中。

```js
func someFunctionThatTakesAClosure(closure: () -> ()) {
    // function body goes here
}
 
// here's how you call this function without using a trailing closure:
 
someFunctionThatTakesAClosure({
    // closure's body goes here
    })
 
// here's how you call this function with a trailing closure instead:
 
someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}

```js

> 注意：
> If a closure expression is provided as the function’s only argument and you provide that expression as a trailing closure, you do not need to write a pair of parentheses () after the function’s name when you call the function.
> 如果函数只有闭包表达式这一个参数，你可以在使用跟尾闭包的时候把（）省略掉。

The string-sorting closure from the Closure Expression Syntax section above can be written outside of the sort function’s parentheses as a trailing closure:

上面的sort函数可以改写为

```js
     reversed = sort(name){$0>$1}
```

Trailing closures are most useful when the closure is sufficiently long that it is not possible to write it inline on a single line. As an example, Swift’s Array type has a map method which takes a closure expression as its single argument. The closure is called once for each item in the array, and returns an alternative mapped value (possibly of some other type) for that item. The nature of the mapping and the type of the returned value is left up to the closure to specify.

跟尾闭包的写法在一些闭包包体逻辑非常长的时候很有用，例如，swift中的array类型有一个map的方法，这个方法只需要一个闭包表达式作为其参数，这个闭包会对数组中每一个元素调用一次，然后返回该函数映射的值（也可能是不同的类型），具体的映射方式和返回值由闭包中的逻辑决定。

After applying the provided closure to each array element, the map method returns a new array containing all of the new mapped values, in the same order as their corresponding values in the original array.

     当提供数组闭包函数之后，map方法将返回一个新的数组，数组中包含了与原数组一一对应的值

Here’s how you can use the map method with a trailing closure to convert an array of Int values into an array of String values. The array [16, 58, 510] is used to create the new array ["OneSix", "FiveEight", "FiveOneZero"]:

    在下面的例子中，你可以使用map函数和跟尾闭包来降数组中的Int值转换成String值。数组[16,58,510]用来创建新的数组[“OneSix”,”FiveEigh”,”FiveOneZero”]:

```js
let digitNames = [
    0: "Zero", 1: "One", 2: "Two",   3: "Three", 4: "Four",
    5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"
]
let numbers = [16, 58, 510]
```
The code above creates a dictionary of mappings between the integer digits and English-language versions of their names. It also defines an array of integers, ready to be converted into strings.

上面的代码使用数字和它所对应的英文字符串创建了一个字典，然后定义了一个数字的数组，用来进行转换。

You can now use the numbers array to create an array of String values, by passing a closure expression to the array’s map method as a trailing closure. Note that the call to numbers.map does not need to include any parentheses after map, because the map method has only one parameter, and that parameter is provided as a trailing closure:

现在你可以使用numers数组来创建一个对应的字符串数组，将一个闭包表达式作为跟尾闭包传递进数组的map函数，在写numbers.map方法的后面不需要添加括号，因为map方法只有一个参数，这个参数已经作为跟尾闭包的形式提供了

```js
let strings = numbers.map {
    (var number) -> String in
    var output = ""
    while number > 0 {
        output = digitNames[number % 10]! + output
        number /= 10
    }
    return output
}
// strings is inferred to be of type String[]
// its value is ["OneSix", "FiveEight", "FiveOneZero"]
```

The map function calls the closure expression once for each item in the array. You do not need to specify the type of the closure’s input parameter, number, because the type can be inferred from the values in the array to be mapped.

map函数将会对数组中的每一个元素调用一次闭包表达式，你不需要制定闭包表达式的输入参数类型，number，因为这个类型可以通过数组中元素的类型来进行推断。

In this example, the closure’s number parameter is defined as a variable parameter, as described in Constant and Variable Parameters, so that the parameter’s value can be modified within the closure body, rather than declaring a new local variable and assigning the passed number value to it. The closure expression also specifies a return type of String, to indicate the type that will be stored in the mapped output array.

这个例子中，闭包中的number参数定义成变量参数（具体参见constans and variable parameters），所以这个参数的值可以在闭包内进行修改。闭包表达式指定了返回值类型为String，表明存储应映射值的新数组类型为String

The closure expression builds a string called output each time it is called. It calculates the last digit of number by using the remainder operator (number % 10), and uses this digit to look up an appropriate string in the digitNames dictionary.

上面的闭包表达式每次被调用的时候创建了一个字符串返回，使用取余运算（number%10)计算最后一位数字并且利用digitNames字段获取对应的字符串。

> 注意：
> The call to the digitNames dictionary’s subscript is followed by an exclamation mark (!), because dictionary subscripts return an optional value to indicate that the dictionary lookup can fail if the key does not exist. In the example above, it is guaranteed that number % 10 will always be a valid subscript key for the digitNames dictionary, and so an exclamation mark is used to force-unwrap the String value stored in the subscript’s optional return value.
> 字典digitNames的下表之后跟着一个惊叹号(!)，因为字典下标返回了一个可选值，表明该Key对应的返回值可能不存在，在上面的例子中，number%10保证了在字典中总会有值对应，因此惊叹号强制取出存储在下表中的String类型

The string retrieved from the digitNames dictionary is added to the front of output, effectively building a string version of the number in reverse. (The expression number % 10 gives a value of 6 for 16, 8 for 58, and 0 for 510.)

从digitNames字段中获取的字符串添加进输出的前部，逆序的建立了一个字符串的数组版本。（再表达式number%10中，如果number为16，则返回6，58则返回8，510返回0）

The number variable is then divided by 10. Because it is an integer, it is rounded down during the division, so 16 becomes 1, 58 becomes 5, and 510 becomes 51.

number变量之后除以10，因为是整数，再计算过程中未除尽的部分会被忽略，因此16变成1，58变成5，510变成了51

The process is repeated until number /= 10 is equal to 0, at which point the output string is returned by the closure, and is added to the output array by the map function.

将整个过程重复，知道number/10变成0，这时闭包会将字符串输出，而map函数则将返回的字符串添加进一个新的映射数组中。

The use of trailing closure syntax in the example above neatly encapsulates the closure’s functionality immediately after the function that closure supports, without needing to wrap the entire closure within the map function’s outer parentheses.

上面的例子中跟尾闭包语法在函数之后将具体的逻辑简介的包装了起来，而不需要将闭包包裹在括号之内

## Capturing Values 捕获值

A closure can capture constants and variables from the surrounding context in which it is defined. The closure can then refer to and modify the values of those constants and variables from within its body, even if the original scope that defined the constants and variables no longer exists.

     闭包可以从变量和常量定义的上下文中捕获他们的值，即使定义他们的域已经不存在了，闭包仍然可以访问和改变他们的值

The simplest form of a closure in Swift is a nested function, written within the body of another function. A nested function can capture any of its outer function’s arguments and can also capture any constants and variables defined within the outer function.

     swift中嵌套函数是闭包最简形式，嵌套函数是定义在其他函数中的函数，它可以捕获外部函数中的所有参数和定义的常量和变量

Here’s an example of a function called makeIncrementor, which contains a nested function called incrementor. The nested incrementor function captures two values, runningTotal and amount, from its surrounding context. After capturing these values, incrementor is returned by makeIncrementor as a closure that increments runningTotal by amount each time it is called.

     这面的makeIncrementor的函数，包含了一个叫做incrementor的嵌套函数，嵌套函数incrementor从上下文中捕获了两个值，runningTotal和amount。之后makeIncrementor将incrementor作为闭包返回，每次调用incrementor时，都会以amount作为增量来增加runningTotal的值

```js
func makeIncrementor(forIncrement amount: Int) -> () -> Int {
var runningTotal = 0
func incrementor() -> Int {
runningTotal += amount
return runningTotal
}
return incrementor
}
```
The return type of makeIncrementor is () -> Int. This means that it returns a function, rather than a simple value. The function it returns has no parameters, and returns an Int value each time it is called. To learn how functions can return other functions, see Function Types as Return Types.

makeIncrementor的返回值类型是()->Int,这表示返回一个函数。这个返回的函数没有其他参数并且每次调用都返回一个Int类型的值。要学习如何在函数中返回其他函数，参见Function Types as Return Types

The makeIncrementor function defines an integer variable called runningTotal, to store the current running total of the incrementor that will be returned. This variable is initialized with a value of 0.

makeIncrementor函数定义了一个整形变量叫做runningTotal.这个变量存储了当前函数的返回值，并且初始化为0.


The makeIncrementor function has a single Int parameter with an external name of forIncrement, and a local name of amount. The argument value passed to this parameter specifies how much runningTotal should be incremented by each time the returned incrementor function is called.

makeIncrementor defines a nested function called incrementor, which performs the actual incrementing. This function simply adds amount to runningTotal, and returns the result.

makeIncrementor定义了一个内嵌函数叫做incrementor,这个函数执行真正的递增逻辑。在这个函数中将amount的值增加到runningTotal中，然后返回它的值。

When considered in isolation, the nested incrementor function might seem unusual:

如果单独拿出来看，内嵌函数incrementor看上起会有点奇怪

```js
func incrementor() -> Int {
    runningTotal += amount
    return runningTotal
}
```

The incrementor function doesn’t have any parameters, and yet it refers to runningTotal and amount from within its function body. It does this by capturing the existing values of runningTotal and amount from its surrounding function and using them within its own function body.

Intrementor函数没有任何参数，他引用的变量runningTotal和amouint来自包含它的函数体，通过捕获外部环境中的变量来实现上面例子中的效果。

Because it does not modify amount, incrementor actually captures and stores a copy of the value stored in amount. This value is stored along with the new incrementor function.

因为没有修改amount参数，incrementor函数实际上是捕获和存储了一个amount的副本，这个值incrementor函数一起存储了起来。

However, because it modifies the runningTotal variable each time it is called, incrementor captures a reference to the current runningTotal variable, and not just a copy of its initial value. Capturing a reference ensures sure that runningTotal does not disappear when the call to makeIncrementor ends, and ensures that runningTotal will continue to be available the next time that the incrementor function is called.

然后，因为它每次调用的时候都修改了runningTotal变量，incrementor捕获了一个指向当前runningTotal变量的引用，不单单只是拷贝了他的初始值。捕获一个引用确保了runningTotal变量不会在makeIncrementor调用结束的时候消失掉，而且确保变量runningTotal在下一次调用的时候也依然可以访问。

> 注意：
> Swift determines what should be captured by reference and what should be copied by value. You don’t need to annotate amount or runningTotal to say that they can be used within the nested incrementor function. Swift also handles all memory management involved in disposing of runningTotal when it is no longer needed by the incrementor function.
>      swift会决定对一个值是保存它的拷贝还是引用。你不需要声明amount和runningTotal他们会在incrementor内嵌函数中使用。swift也会处理所有的内存管理，当runningTotal不再需要的时候会将它释放掉。

Here’s an example of makeIncrementor in action:

这里是makeIncrementor的一个例子

```js
let incrementByTen = makeIncrementor(forIncrement: 10)
```

This example sets a constant called incrementByTen to refer to an incrementor function that adds 10 to its runningTotal variable each time it is called. Calling the function multiple times shows this behavior in action:

这个例子将一个叫做incrementByTen的常量保存10与runningTotal变量每次想加的引用。调用函数多次来查看结果:

```js
incrementByTen()
// returns a value of 10
incrementByTen()
// returns a value of 20
incrementByTen()
// returns a value of 30
```

If you create another incrementor, it will have its own stored reference to a new, separate runningTotal variable. In the example below, incrementBySeven captures a reference to a new runningTotal variable, and this variable is unconnected to the one captured by incrementByTen:

如果你创建另外一个incrementor，它会有一个新的引用于之前的runningTotal完全分离，下面这个例子里面incrementBySeven捕获了一个新的runningTotal变量，这个变量跟incrementByTen捕获的没有任何联系

```js
let incrementBySeven = makeIncrementor(forIncrement: 7)
incrementBySeven()
// returns a value of 7
incrementByTen()
// returns a value of 40
```

> 注意
> If you assign a closure to a property of a class instance, and the closure captures that instance by referring to the instance or its members, you will create a strong reference cycle between the closure and the instance. Swift uses capture lists to break these strong reference cycles. For more information, see Strong Reference Cycles for Closures.
>      如果你在闭包里访问了一个类实例的属性，闭包会捕获这个实例或者成员函数的引用，你会创建一个互相强引用的环，swift使用捕获列表来打破这个互相引用的环，详情请看Strong Reference Cycles for Closures.

## Closures Are Reference Types 闭包都是引用类型

In the example above, incrementBySeven and incrementByTen are constants, but the closures these constants refer to are still able to increment the runningTotal variables that they have captured. This is because functions and closures are reference types.

     上面的例子里面incrementBySeven和incrementByTen都是常量，但是这些常量引用的闭包仍然可以增加他们捕获的runningTotal变量的值，这是因为函数和闭包都是引用类型。

Whenever you assign a function or a closure to a constant or a variable, you are actually setting that constant or variable to be a reference to the function or closure. In the example above, it is the choice of closure that incrementByTen refers to that is constant, and not the contents of the closure itself.

     任何时候当你将一个函数或者闭包赋值给一个常量或者变量，实际上你将这个闭包的引用设置给了这个常量或者变量。上面的例子中，变成常量的是这个闭包的引用，而不是只它的包体内包含的内容。

This also means that if you assign a closure to two different constants or variables, both of those constants or variables will refer to the same closure:

     这意味着如果你将一个闭包赋值给两个不同的变量和常量，他们都会指向同一个闭包

```js
       let alsoIncrementByTen = incrementByTen
               alsoIncrementByTen()
               // returns a value of 50
```
