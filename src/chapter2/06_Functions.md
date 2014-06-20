# Functions
# 函数

Functions are self-contained chunks of code that perform a specific task. You give a function a name that identifies what it does, and this name is used to “call” the function to perform its task when needed.

函数是执行特定任务的独立代码块。你可以给函数起一个名字来标识它的功能，并在需要时使用这个名字来“调用”该函数执行任务。

Swift’s unified function syntax is flexible enough to express anything from a simple C-style function with no parameter names to a complex Objective-C-style method with local and external parameter names for each parameter. Parameters can provide default values to simplify function calls and can be passed as in-out parameters, which modify a passed variable once the function has completed its execution.

Swift的统一标准函数语法足够灵活来表达一切，从简单的无参数名的C风格函数到复杂的每个参数都有本地和外部参数名的Objective-C风格方法。可以为参数提供默认值来简化函数调用，也可以为参数传入in-out参数，一旦函数完成执行，传入的变量会被修改。

Every function in Swift has a type, consisting of the function’s parameter types and return type. You can use this type like any other type in Swift, which makes it easy to pass functions as parameters to other functions, and to return functions from functions. Functions can also be written within other functions to encapsulate useful functionality within a nested function scope.

Swift的每个函数都有类型，包含函数参数类型和返回类型。你可以像swift中任何其他类型那样使用，这让函数作为参数传递给其他函数，和从函数返回函数变得十分容易。函数也可以定义在另一个函数中， 在嵌套函数范围内，封装特定功能。

Defining and Calling Functions

定义和调用函数

When you define a function, you can optionally define one or more named, typed values that the function takes as input (known as parameters), and/or a type of value that the function will pass back as output when it is done (known as its return type).

定义函数时，你可以为其定义一个或多个具有名称、类型的值作为输入（称为参数），和/或该函数执行完毕后传回的一个有类型的值作为输出（称为返回值）。

Every function has a function name, which describes the task that the function performs. To use a function, you “call” that function with its name and pass it input values (known as arguments) that match the types of the function’s parameters. A function’s arguments must always be provided in the same order as the function’s parameter list.

每个函数都有一个函数名用来描述此函数运行的任务。使用函数时，通过函数名并传入符合函数参数类型的输入值（称为参数）来“调用”函数。必须按照函数参数列表相同的顺序提供函数参数。

The function in the example below is called greetingForPerson, because that’s what it does—it takes a person’s name as input and returns a greeting for that person. To accomplish this, you define one input parameter—a String value called personName—and a return type of String, which will contain a greeting for that person:

下面例子中的函数叫做sayHello，因为这就是它的功能——它以人名作为输入，并返回对这个人的问候（greeting）。为了实现这一点，需要定义一个输入参数——一个名为personName的字符串值，和一个字符串类型的返回值带有对此人的问候。

```js
func sayHello(personName: String) -> String {
    let greeting = "Hello, " + personName + "!"
    return greeting
}
```

All of this information is rolled up into the function’s definition, which is prefixed with the func keyword. You indicate the function’s return type with the return arrow -> (a hyphen followed by a right angle bracket), which is followed by the name of the type to return.

所有这些信息构成了一个函数的定义，并以 func 关键字作为前缀。使用返回箭头->（连字符后跟一个右尖括号）和紧接着的返回类型名来声明函数的返回类型。

The definition describes what the function does, what it expects to receive, and what it returns when it is done. The definition makes it easy for the function to be called elsewhere in your code in a clear and unambiguous way:

函数定义描述这个函数是做什么的，期望接收什么和运行结束后返回什么。这个定义使得在代码中任何地方用清晰明白的方式调用函数变得容易。

```js

println(sayHello("Anna"))
// prints "Hello, Anna!"
println(sayHello("Brian"))
// prints "Hello, Brian!”
```

You call the sayHello function by passing it a String argument value in parentheses, such as sayHello("Anna"). Because the function returns a String value, sayHello can be wrapped in a call to the println function to print that string and see its return value, as shown above.

通过在括号中传入一个字符串参数值来调用sayHello函数，如sayHello(“Anna”)。由于函数返回了一个字符串类型的值，sayHello可以包装在 println 函数中，用来打印这个字符串并查看它的返回值，如上所示。

The body of the sayHello function starts by defining a new String constant called greeting and setting it to a simple greeting message for personName. This greeting is then passed back out of the function using the return keyword. As soon as return greeting is called, the function finishes its execution and returns the current value of greeting.

sayHello 函数的主体始于定义一个名为 greeting 的字符串常量，并为它设置对personName的简单问候信息。然后通过 return 关键字把 greeting 传出函数。一旦执行了 return greeting，函数结束执行并返回当前的greeting值。

You can call the sayHello function multiple times with different input values. The example above shows what happens if it is called with an input value of "Anna", and an input value of "Brian". The function returns a tailored greeting in each case.

你可以传入不同的输入值多次调用 sayHello 函数。上述例子展示了输入值为“Anna”和“Brian”时发生了什么。每个例子中函数返回了定制的greeting。

To simplify the body of this function, combine the message creation and the return statement into one line:

为了简化函数体，可以把消息创建和返回语句合并为一行：

```js
func sayHelloAgain(personName: String) -> String {
    return "Hello again, " + personName + "!"
}
println(sayHelloAgain("Anna"))
// prints "Hello again, Anna!”
```

Function Parameters and Return Values
函数参数和返回值
