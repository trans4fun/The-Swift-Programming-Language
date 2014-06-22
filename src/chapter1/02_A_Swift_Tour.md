A Swift Tour

Tradition suggests that the first program in a new language should print the words “Hello, world” on the screen. In Swift, this can be done in a single line:
通常学习一门新语言都会输出一行“Hello,world”.在swift里只需要一行代码

“If you have written code in C or Objective-C, this syntax looks familiar to you—in Swift, this line of code is a complete program. You don’t need to import a separate library for functionality like input/output or string handling. Code written at global scope is used as the entry point for the program, so you don’t need a main function. You also don’t need to write semicolons at the end of every statement.”
如果你之前写过C或者Objective-C的代码，你会很熟悉这种语法。在swift里，这一行代码就是一个完整的程序，你不需要再去引入一个完成类似输入输出，字符串处理等操作的类库。在全局范围内编写的代码就是程序的入口，因此你不再需要main函数了，也不需要在每一条语句末尾写分号。

“This tour gives you enough information to start writing code in Swift by showing you how to accomplish a variety of programming tasks. Don’t worry if you don’t understand something—everything introduced in this tour is explained in detail in the rest of this book.”
这篇文章会充分向你展示如何用swift完成各种编程任务。不用担心一些细节不太理解，在这本书之后的章节中会详细的为你介绍。


“Simple Values
Use let to make a constant and var to make a variable. The value of a constant doesn’t need to be known at compile time, but you must assign it a value exactly once. This means you can use constants to name a value that you determine once but use in many places.”
简单值
使用let声明常量，var声明变量。在编译的时候不需要知道常量的值，但是你只能给常量显式地赋值一次。也就是说你可以给常量赋一次值然后在其他一些地方来使用。

“A constant or variable must have the same type as the value you want to assign to it. However, you don’t always have to write the type explicitly. Providing a value when you create a constant or variable lets the compiler infer its type. In the example above, the compiler infers that myVariable is an integer because its initial value is a integer.”
不管是常量还是变量必须与其所赋的值类型保持一致。你不一定要把常量或者变量的类型显式地写出来。因为编译器可以根据值来自动推断常量或者变量的类型。如上面的例子，编译器根据myVariable的初始值类型推断出它是一个整型变量。

“If the initial value doesn’t provide enough information (or if there is no initial value), specify the type by writing it after the variable, separated by a colon.”
如果初始值没有提供足够的信息或者没有初始值，可以在变量后面写上它的类型，变量和类型用冒号隔开。

“Values are never implicitly converted to another type. If you need to convert a value to a different type, explicitly make an instance of the desired type.”
值的类型不会自动转换，如果你需要把一个值转换成另外一种类型，需要强制转换。

“There’s an even simpler way to include values in strings: Write the value in parentheses, and write a backslash (\) before the parentheses. For example:”
有一种更简单的把值转换成字符串的方法：把值写在括号里，然后在括号前加一个反斜杠。例如：

“Create arrays and dictionaries using brackets ([]), and access their elements by writing the index or key in brackets.”
用中括号创建数组和字典，通过中括号里的索引和键来访问集合中的元素。

“To create an empty array or dictionary, use the initializer syntax.”
用下面的初始化语法来创建一个空的数组或字典

“If type information can be inferred, you can write an empty array as [] and an empty dictionary as [:]—for example, when you set a new value for a variable or pass an argument to a function.”
如果类型可以被推断出来，你可以用[]来创建一个空数组，用[:]来创建一个空字典。例如，当你给一个变量赋值或者给一个函数传参

“Control Flow
Use if and switch to make conditionals, and use for-in, for, while, and do-while to make loops. Parentheses around the condition or loop variable are optional. Braces around the body are required.”
流控制
使用if和switch来进行条件控制，使用for-in、for、while和do-while来进行循环控制。条件和循环变量外面的括号可以省略，但是语句体的大括号是必须的。

“In an if statement, the conditional must be a Boolean expression—this means that code such as if score { ... } is an error, not an implicit comparison to zero.”
在if语句里，条件必须是一个Boolean表达式。所以if score { ... }这种写法是错误的，score不会隐式地和0来比较。

“You can use if and let together to work with values that might be missing. These values are represented as optionals. An optional value either contains a value or contains nil to indicate that the value is missing. Write a question mark (?) after the type of a value to mark the value as optional.”
你可以一起使用if和let来处理值缺失的情况。有些变量的值是可选的。一个可选的值可能是一个具体的值或者是nil，表示值缺失。在类型后面加一个问号来标记这个变量的值是可选的。

“If the optional value is nil, the conditional is false and the code in braces is skipped. Otherwise, the optional value is unwrapped and assigned to the constant after let, which makes the unwrapped value available inside the block of code.”
如果变量的可选值是nil，则判断条件为false，大括号中的代码被略过。如果不为nil，可选值会赋值给let后的常量，并且该常量可以在代码块中使用。

“Switches support any kind of data and a wide variety of comparison operations—they aren’t limited to integers and tests for equality.”
Switch支持各种类型的数据以及大量的比较操作-它们不仅限于整数和比较大小。

“After executing the code inside the switch case that matched, the program exits from the switch statement. Execution doesn’t continue to the next case, so there is no need to explicitly break out of the switch at the end of each case’s code.”
与switch的case相匹配的代码执行完之后，程序不会继续执行下一个case中的代码，而是会自动退出switch语句，所以不需要在每一个case的代码后面显式的调用break。

“You use for-in to iterate over items in a dictionary by providing a pair of names to use for each key-value pair.”
你可以使用for-in来遍历字典，用两个变量来表示每对键值。

“Use while to repeat a block of code until a condition changes. The condition of a loop can be at the end instead, ensuring that the loop is run at least once.”
使用while来重复执行一段代码直到条件改变。循环条件也可也在末尾，以保证循环至少可执行一次。

“You can keep an index in a loop—either by using .. to make a range of indexes or by writing an explicit initialization, condition, and increment. These two loops do the same thing:”
在循环中可以使用..来表示索引范围或者使用传统的方式。两者是等价的。

“Use .. to make a range that omits its upper value, and use ... to make a range that includes both values.”
使用..会忽略范围中的上限值，使用...则不会忽略。

“Functions and Closures
Use func to declare a function. Call a function by following its name with a list of arguments in parentheses. Use -> to separate the parameter names and types from the function’s return type.”
函数和闭包
使用func来声明一个函数。在函数名后的括号里加入参数来调用函数。使用->分隔开函数的参数和函数的返回值类型。

“Use a tuple to return multiple values from a function.”
使用元组来返回一组值。

“Functions can also take a variable number of arguments, collecting them into an array.”
函数可以有一组可变个数的参数，由array来表示。

“Functions can be nested. Nested functions have access to variables that were declared in the outer function. You can use nested functions to organize the code in a function that is long or complex.”
函数可以嵌套，被嵌套的函数可以访问外部函数中声明的变量。你可以使用嵌套函数来重构一段很长很复杂的函数。

“Functions are a first-class type. This means that a function can return another function as its value.”
函数是first-class类型，因此它可以作为另一个函数的返回值。

“A function can take another function as one of its arguments.”
函数可以作为另一个函数的参数。

“Functions are actually a special case of closures. You can write a closure without a name by surrounding code with braces ({}). Use in to separate the arguments and return type from the body.”
函数实际上是一个特殊的闭包。你可以把一段代码写在大括号{}中来表示一个匿名闭包，参数和返回类型与闭包体之间用in来分隔。

“You have several options for writing closures more concisely. When a closure’s type is already known, such as the callback for a delegate, you can omit the type of its parameters, its return type, or both. Single statement closures implicitly return the value of their only statement.”
有一些简洁表示闭包的方式。当一个闭包的类型已知，例如作为委托的回调，可以省略它的参数和返回类型。单个语句闭包会把它语句的值当做结果返回。

“You can refer to parameters by number instead of by name—this approach is especially useful in very short closures. A closure passed as the last argument to a function can appear immediately after the parentheses.”
你可以使用参数位置替代参数名来引用参数-这个方法特别是在很短的闭包里很好用。闭包作为函数最后一个参数的时候，可以直接跟在小括号后面。

“Objects and Classes
Use class followed by the class’s name to create a class. A property declaration in a class is written the same way as a constant or variable declaration, except that it is in the ”
“context of a class. Likewise, method and function declarations are written the same way.”
对象和类
使用class和类名来创建一个类。类中的属性声明是和常量或者变量的声明方式一样的，唯一的区别是属性声明是在类的上下文之中的。同样的，方法和函数的声明也是一样的。

“Create an instance of a class by putting parentheses after the class name. Use dot syntax to access the properties and methods of the instance.”
类名后面跟小括号来创建一个类的实例。使用点语法来访问该实例的属性和方法。

“This version of the Shape class is missing something important: an initializer to set up the class when an instance is created. Use init to create one.”
这个版本的Shape类缺少了一个重要的东西：类实例化时候的一个构造器。使用init来创造一个构造器。

“Notice how self is used to distinguish the name property from the name argument to the initializer. The arguments to the initializer are passed like a function call when you create an instance of the class. Every property needs a value assigned—either in its declaration (as with numberOfSides) or in the initializer (as with name).”
注意用self来区分name属性和传递给构造器的name参数。像函数调用一样，把参数传递给构造器来创建一个类实例。每一个属性都需要赋值，在属性的声明中（如numberOfSides），或者在构造器中（如name）

“Use deinit to create a deinitializer if you need to perform some cleanup before the object is deallocated.”
“Subclasses include their superclass name after their class name, separated by a colon. There is no requirement for classes to subclass any standard root class, so you can include or omit a superclass as needed.”
使用deinit来创建一个析构器来执行对象销毁前的清理工作。
定义子类的时候是在类名后加上父类的名字，中间用冒号隔开。因为类不需要继承任何标准的基类，所以你可以省略父类。

“Methods on a subclass that override the superclass’s implementation are marked with override—overriding a method by accident, without override, is detected by the compiler as an error. The compiler also detects methods with override that don’t actually override any method in the superclass.”
子类方法重写父类方法的时候标记为override-这是为了防止意外的重写，如果没有override关键字，编译器会报错。编译器同样会检测在子类标记为override的方法是否真的重写了父类的某个方法。

“In addition to simple properties that are stored, properties can have a getter and a setter.”
属性也可以有getter和setter方法。

“In the setter for perimeter, the new value has the implicit name newValue. You can provide an explicit name in parentheses after set.”
在setter方法中，新的属性值被隐式地命名为newValue。你可以在set后的括号里显式地给属性值命名。

“Notice that the initializer for the EquilateralTriangle class has three different steps:
Setting the value of properties that the subclass declares.
Calling the superclass’s initializer.
Changing the value of properties defined by the ”
“superclass. Any additional setup work that uses methods, getters, or setters can also be done at this point.”
注意创建EquilateralTriangle类的构造器包含三个不同的步骤。
1.在子类声明的时候设置属性值。
2.调用父类的构造器。
3.改变定义在父类中的属性值，还有调用方法，getter和setter方法都可以在这个步骤完成。

“If you don’t need to compute the property but still need to provide code that is run before and after setting a new value, use willSet and didSet. For example, the class below ensures that the side length of its triangle is always the same as the side length of its square.”
如果你不需要计算属性，但仍需要在给属性设置新值的前后运行一些代码，使用willSet和didSet。例如，下面的类会确保三角形的边长和方形的边长相等。

“Methods on classes have one important difference from functions. Parameter names in functions are used only within the function, but parameters names in methods are also used when you call the method (except for the first parameter). By default, a method has the same name for its parameters when you call it and within the method itself. You can specify a second name, which is used inside the method.”
类中的方法和函数有一个很重要的区别。函数中的参数只会在函数内部使用，但是方法中的参数还可以在方法调用的时候使用（除了第一个参数）。默认情况下，方法调用时候的参数名和方法内部使用的参数名保持一致。在方法内部使用的时候你也可以定义一个不同的名字。

“When working with optional values, you can write ? before operations like methods, properties, and subscripting. If the value before the ? is nil, everything after the ? is ignored and the value of the whole expression is nil. Otherwise, the optional value is unwrapped, and everything after the ? acts on the unwrapped value. In both cases, the value of the whole expression is an optional value.”
处理可选值的时候，你可以在？后面跟上方法，属性，子脚本等操作。如果？之前的值是nil，？后面的代码会被忽略，然后整个表达式的值返回nil。否则，？之后的代码会执行。在这两种情况下，整个表达式就是一个可选值。

“Enumerations and Structures
Use enum to create an enumeration. Like classes and all other named types, enumerations can have methods associated with them.”
枚举和结构体
使用enum来创建一个枚举。像类和其他命名类型一样，枚举可以有方法。

“In the example above, the raw value type of the enumeration is Int, so you only have to specify the first raw value. The rest of the raw values are assigned in order. You can also use strings or floating-point numbers as the raw type of an enumeration.”
在上面的例子中，枚举的原始值类型是Int，所以你只需要指定第一个值，其余的会按照顺序进行赋值。你同样可以使用字符串和浮点数作为枚举的原始类型。

“Use the toRaw and fromRaw functions to convert between the raw value and the enumeration value.”
使用toRaw和fromRaw这两个函数用于在原始值和枚举值之间转换。

“The member values of an enumeration are actual values, not just another way of writing their raw values. In fact, in cases where there isn’t a meaningful raw value, you don’t have to provide one.”
枚举的成员值是实际值，并不是原始值的另一种表示方式。实际上，如果原始值没有意义，你就不需要提供。

“Notice the two ways that the Hearts member of the ”
“enumeration is referred to above: When assigning a value to the hearts constant, the enumeration member Suit.Hearts is referred to by its full name because the constant doesn’t have an explicit type specified. Inside the switch, the enumeration is referred to by the abbreviated form .Hearts because the value of self is already known to be a suit. You can use the abbreviated form anytime the value’s type is already known.”
注意，有两种方式可以引用Hearts成员：当给hearts常量赋值时，通过Suit.Hearts全名来引用枚举成员，因为常量没有显式指定其类型。在switch语句内部，因为已知self是一个suit，所以可以通过.Hearts这种简写的方式来引用枚举。在已知值类型的情况下你都可以采用简写的方式。

“Use struct to create a structure. Structures support many of the same behaviors as classes, including methods and initializers. One of the most important differences between structures and classes is that structures are always copied when they are passed around in your code, but classes are passed by reference.”
使用struct来创建一个结构体。结构体支持很多和类同样的操作，包括方法和构造器。两者之间最重要的差别是结构体在代码中传递采用的是拷贝的方式，但是类采用的是传递引用的方式。

“An instance of an enumeration member can have values associated with the instance. Instances of the same enumeration member can have different values associated with them. You provide the associated values when you create the instance. Associated values and raw values are different: The raw value of an enumeration member is the ”“same for all of its instances, and you provide the raw value when you define the enumeration.”
一个枚举成员的实例可以有对应的实例值。相同枚举成员的实例可以有不同的实例值。当你创建一个实例的时候提供对应的实例值。实例值和原始值是不同的：枚举成员所有的实例的原始值都是相同的，而且你是在定义枚举的时候提供原始值。

“For example, consider the case of requesting the sunrise and sunset time from a server. The server either responds with the information or it responds with some error information.”
例如，考虑从服务端获取日出和日落的时间。服务端要么返回正常信息，要么返回错误信息。

“Notice how the sunrise and sunset times are extracted from the ServerResponse value as part of matching the value against the switch cases.”
注意，如何从ServerResponse中提去日出和日落时间。

Protocols and Extensions
“Use protocol to declare a protocol.”
协议和扩展
使用protocol来声明一个协议

“Classes, enumerations, and structs can all adopt protocols.”
类，枚举，结构体都可以遵循协议

“Notice the use of the mutating keyword in the declaration of SimpleStructure to mark a method that modifies the structure. The declaration of SimpleClass doesn’t need any of its methods marked as mutating because methods on a class can always modify the class.”
注意，在SimpleStructure的声明中使用关键字mutating来标记一个会修改结构体的方法。在SimpleClass的声明中不需要用关键字mutating来标记类中的方法，因为类中的方法总是可以修改类。

“Use extension to add functionality to an existing type, such as new methods and computed properties. You can use an extension to add protocol conformance to a type that is declared elsewhere, or even to a type that you imported from a library or framework.”
使用扩展给一个已存在的类型增加功能，例如一些新方法和计算过的属性。你可以使用扩展给一个在别处声明的类型增加协议，甚至是给一个从库和框架中引入的类型增加协议。

“You can use a protocol name just like any other named type—for example, to create a collection of objects that have different types but that all conform to a single protocol. When you work with values whose type is a protocol type, methods outside the protocol definition are not available.”
你可以像使用其他命名类型一样使用协议名-例如，创建一个具有不同类型但是遵循同一协议的对象集合。当你处理一些协议类型的值的时候，协议定义之外的方法是不可用的。

“Even though the variable protocolValue has a runtime type of SimpleClass, the compiler treats it as the given type of ExampleProtocol. This means that you can’t accidentally access methods or properties that the class implements in addition to its protocol conformance.”
虽然变量protocolValue具有一个运行时类型SimpleClass，编译器是把它当做一个协议类型来处理的。这意味着你不能够访问协议没有指定的方法和属性。

Generics
“Write a name inside angle brackets to make a generic function or type.”
泛型
在尖括号中写一个名字来创建一个泛型函数或类型。

“You can make generic forms of functions and methods, as well as classes, enumerations, and structures.”
你可以使用泛型来创建函数，方法，类，枚举和结构体。

“Use where after the type name to specify a list of ”
“requirements—for example, to require the type to implement a protocol, to require two types to be the same, or to require a class to have a particular superclass.”
在类型名之后使用where来指定一些条件-例如，要求类型遵循某个协议，要求两个类型相同，或者要求一个类有一个特定的父类。

“In the simple cases, you can omit where and simply write the protocol or class name after a colon. Writing <T: Equatable> is the same as writing <T where T: Equatable>.”
在简单情况下，你可以省略where，然后在协议和类名之间用冒号隔开。 <T: Equatable>和<T where T: Equatable>是等价的。
