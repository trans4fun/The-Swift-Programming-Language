# Types
# 类型

In Swift, there are two kinds of types: named types and compound types. A named type is a type that can be given a particular name when it is defined. Named types include classes, structures, enumerations, and protocols. For example, instances of a user-defined class named MyClass have the type MyClass. In addition to user-defined named types, the Swift standard library defines many commonly used named types, including those that represent arrays, dictionaries, and optional values.

在swift里，有两种类型：命名类型和复合类型。命名类型是指当它被定义的时候能够给一个指定名字的类型。命名类型包含类、结构、枚举和协议。例如，用户定义的类的实例MyClass，其类型就是MyClass。除了用户定义的命名类型，swift标准库还定义了很多常用命名类型，<b>包含的代表有数组，字典，可选值。</b>


Data types that are normally considered basic or primitive in other languages—such as types that represent numbers, characters, and strings—are actually named types, defined and implemented in the Swift standard library using structures. Because they are named types, you can extend their behavior to suit the needs of your program, using an extension declaration, discussed in Extensions and Extension Declaration.


通常被其它语言视为是最基础或最原始的数据类型，例如数字、字符、字符串，实际上都是命名类型，swift标准库使用结构去定义和实现他们。因为他们是命名类型，你可以用扩展声明来扩展他们的行为，以满足你的程序需求，详细讨论请参考‘扩展和扩展声明’。


A compound type is a type without a name, defined in the Swift language itself. There are two compound types: function types and tuple types. A compound type may contain named types and other compound types. For instance, the tuple type (Int, (Int, Int)) contains two elements: The first is the named type Int, and the second is another compound type (Int, Int).

复合类型是一个没有名字的类型，由swift内部自己定义。swift有两种复合类型：函数类型和元组类型。一个复合数据类型可以包含命名类型和其他复合类型。例如，一个元组类型（Int, (Int, Int)）包含两个元素：第一个是命名类型Int,第二个是复合类型（Int, Int）。

This chapter discusses the types defined in the Swift language itself and describes the type inference behavior of Swift.

本章讨论swif语言本身定义的类型，<b>描述在swift中类型推断的方式</b>。

> GRAMMAR OF A TYPE
> 
> 类型的语法

> type → array-type  function-type  type-identifier tuple-type  optional-type  implicitly-unwrapped-optional-type  protocol-composition-type  metatype-type
> 
> type -> 数组类型｜函数类型｜类型标识｜元组类型｜可选类型｜隐式去包装可选类型｜<b>协议构成类型</b>｜元型类型
        
        
## Type Annotation    
     
## 类型注释
A type annotation explicitly specifies the type of a variable or expression. Type annotations begin with a colon (:) and end with a type, as the following examples show:

类型标注明确的指定一个变量或者表达式的类型。类型注释以冒号(:)开始，类型结束，如下面的列子：


        1. let someTuple:(Double, Double) = (3.14159, 2.71828)
    
        2. func someFunction(a:Int) { /**/}

In the first example, the expression someTuple is specified to “have the tuple type (Double, Double). In the second example, the parameter a to the function someFunction is specified to have the type Int.

在第一个例子中，表达式someTuple是被指定为元组类型(Double, Double)。在第二个例子中，函数someFuncion的参数a被指定为Int类型。

Type annotations can contain an optional list of type attributes before the type.

类型注释可以在类型前面包含一个<b>类型属性</b>的可选列表。

> GRAMMAR OF A TYPE ANNOTATION

> 类型注释的语法

> type-annotation → :attributesopttyp
> type-annotation -> :属性［可选］类型
    

## Type Identifier 
## 类型标识符

A type identifier refers to either a named type or a type alias of a named or compound type.

<b>类型标识符是指一个命名类型、命名类型的别名或复合类型。</b>

Most of the time, a type identifier directly refers to a named type with the same name as the identifier. For example, Int is a type identifier that directly refers to the named type Int, and the type identifier Dictionary<String, Int> directly refers to the named type Dictionary<String, Int>.

大多数情况下，类型标识符是指向相同名字的命名类型。例如，类型标识符Int指向命名类型Int,类型标识符Dictionary<String, Int>指向命名类型Dictionary<String, Int>。

There are two cases in which a type identifier does not refer to a type with the same name. In the first case, a type identifier refers to a type alias of a named or compound type. For instance, in the example below, the use of Point in the “type annotation refers to the tuple type (Int, Int).

命名标识符和类型不同名的情况有两种。第一种情况，命名标识符指向命名类型的别名或者复合类型。例如下面的例子，类型标识符使用Point指向元组类型(Int, Int)。

        typealias Point = (Int, Int);
        let origin: Point = (0, 0);
    

In the second case, a type identifier uses dot (.) syntax to refer to named types declared in other modules or nested within other types. For example, the type identifier in the following code references the named type MyType that is declared in the ExampleModule module.

第二种情况，类型标识符用点（.）的语法指向声明在其它模块或在其它类型中嵌套的命名类型。例如，在下面的代码中，类型标识符引用在模块ExampleModule中声明的命名类型MyType。

        var someValue: ExampleModule.MyType    
    

> GRAMMAR OF A TYPE IDENTIFIER
> 
> 命名标识符的语法

‌> type-identifier → type-namegeneric-argument-clauseopt type-namegeneric-argument-clauseopt.type-identifier

> 命名标识符 -> 类型名称 泛型参数子句［可选］｜类型名称 泛型参数子句［可选］.类型标识符
> 
> type-name → identifier”

> 类型标识符 -> 标识符


## Tuple Type
## 元组类型

A tuple type is a comma-separated list of zero or more types, enclosed in parentheses.

元组类型是指在括号中，以逗号分隔的零到多个类型的列表。

You can use a tuple type as the return type of a function to enable the function to return a single tuple containing “multiple values. You can also name the elements of a tuple type and use those names to refer to the values of the individual elements. An element name consists of an identifier followed immediately by a colon (:). For an example that demonstrates both of these features, see Functions with Multiple Return Values.

你可以用元组类型作为函数的返回值类型，这样函数就能返回包含多个值的单元组。你也可以给元组类型中的元素命名，用这些名字来引用单个元素的值。元素的名字由标识符和紧跟着的冒号(:)组成。这两种特性的例子演示，请看 ‘多个返回值的函数’。


Void is a typealias for the the empty tuple type, (). If there is only one element inside the parentheses, the type is simply the type of that element. For example, the type of (Int) is Int, not (Int). As a result, you can label a tuple element only when the tuple type has two or more elements.


Void是空元组类型的别名，()。如果在括号里面只有一个元素，那么这个类型就是元素的类型。例如,(Int)的类型是Int，不是(Int)。因此，你可以认为仅当元组类型包含两个或者更多元素的时候才是元组元素。

 
> GRAMMAR OF A TUPLE TYPE
> 
> 元组类型的语法
> 
> tuple-type → (tuple-type-bodyopt)

> 元组类型 -> (元组类型体［可选］)

> tuple-type-body → tuple-type-element-list...opt

> 元组类型体 -> 元组类型元素列表...［可选］

> tuple-type-element-list → tuple-type-element  tuple-type-element,tuple-type-element-list

> 元组类型元素列表 -> 元组类型元素｜元组类型元素，元组类型元素列表

> tuple-type-element → attributesoptinoutopttype inoutoptelement-nametype-annotation

> 元组类型元素 -> 属性［可选］inout［可选］类型｜inout［可选］元素名称 类型注释

> element-name → identifier

> 元素名称 -> 标识符
    

## Function Type
## 函数类型

A function type represents the type of a function, method, or closure and consists of a parameter and return type separated by an arrow (->):

函数类型表示一个函数，方法，闭包的类型，它由参数和返回类型组成，中间通过箭头(->)分隔：

        parameter type -> return type
    
Because the parameter type and the return type can be a tuple type, function types support functions and methods that take multiple paramaters and return multiple values.

因为参数类型和返回类型都可以为元组类型，所以函数类型支持函数和方法有多个参数和多个返回值。

You can apply the auto_closure attribute to a function type that has a parameter type of () and that returns the type of an expression (see Type Attributes). An autoclosure function captures an implicit closure over the specified expression, instead of the expression itself. The following example uses the auto_closure attribute in defining a very simple assert function:


<b>你可以为参数类型为()，返回值为表达式类型的函数类型申请auto_closure属性(请看 ’类型属性‘)。一个自动闭包函数捕获的是指定表达式上的隐式闭包而不是表达式本身。</b>下面的例子用auto_closure属性定义一个简单的assert函数：

        func simpleAssert(condition: @auto_closure () -> Bool, message: String){
            if !condition(){
                println(message)
            }
        }
        let testNumber = 5
        simpleAssert(testNumber % 2 == 0, "testNumber isn't an even number.")
        // prints "testNumber isn't an even number."


A function type can have a variadic parameter as the last parameter in its parameter type. Syntactically, a variadic parameter consists of a base type name followed immediately by three dots (...), as in Int.... A variadic parameter is treated as an array that contains elements of the base type name. For instance, the variadic parameter Int... is treated as Int[]. For an example that uses a variadic parameter, see Variadic Parameters.

<b>一个函数类型的参数类型里可以让一个可变参数作为其最后一个参数。</b> 从语法上来说，可变参数可以由一个基础类型名称和紧跟着的三个点(...)组成，例如Int...。可变参数被认为是一个包含基础类型名称的数组。例如，可变参数Int... 被认为是Int[]。使用可变参数的例子，请参考 ‘可变参数’。

To specify an in-out parameter, prefix the parameter type with the inout keyword. You can’t mark a variadic parameter or a return type with the inout keyword. In-out parameters are discussed in In-Out Parameters.

指定一个in-out参数，需要给参数类型加上inout的前缀。可变参数和返回类型不能使用inout标记。in-out参数在’In-Out参数‘中有讨论。

The type of a curried function is equivalent to a nested function type. For example, the type of the curried function addTwoNumbers()() below is Int -> Int -> Int:

柯里化函数（curried function）类型相当于嵌套函数类型。例如，下面的柯里化函数addTwoNumbers()()的类型是Int -> Int -> Int:


        func addTwoNumbers(a: Int)(b: Int) -> Int{
            return a + b
        }
    
        addTwoNumbers(4)(5)      // returns 9


The function types of a curried function are grouped from right to left. For instance, the function type Int -> Int -> Int is understood as Int -> (Int -> Int)—that is, a function that takes an Int and returns another function that takes and return an Int. For example, you can rewrite the curried function addTwoNumbers()() as the following nested function:

柯里化函数的函数类型从右到左形成一组。例如，函数类型Int -> Int -> Int被理解为Int ->  (Int -> Int) -- 指函数传入一个Int，然后返回另外一个输入输出都是Int的函数。

         func addTwoNumbers(a: Int) -> (Int -> Int){
            func addTheSecondNumber(b: Int) -> Int{
                return a + b
            }
            return addTheSecondNumber
        }
    
        addTwoNumbers(4)(5)     // Returns 9
    

> GRAMMAR OF A FUNCTION TYPE

> 函数类型的语法

> function-type → type->type”

> 函数类型 → 类型 -> 类型
    
   
## Array Type  
## 数组类型

The Swift language uses square brackets ([]) immediately after the name of a type as syntactic sugar for the named type Array<T>, which is defined in the Swift standard library. In other words, the following two declarations are equivalent:

在swift中类型紧跟着[]作为标准库定义的命名类型Array<T>的简写。换句话说，下面两个声明是相等的：

    let someArray: String[] = ["Alex", "Brian", "Dave"]
    let someArray: Array<String> = ["Alex", "Brian", "Dave"]

In both cases, the constant someArray is declared as an array of strings. The elements of an array can be accessed using square brackets as well: someArray[0] refers to the element at index 0, "Alex".

在这两种情况下，常量someArray被定义为字符串数组。数组元素也可以用中括号访问：someArray[0] 指向index为0的元素，即‘Alex’。

As the above example also shows, you can use square brackets to create an array using an array literal. Empty array literals are written using an empty pair of square brackets and can be used to create an empty array of a specified type.

<b>如上面的例子显示，你可以利用数组自变量通过[]创建一个数组。</b>空数组自变量用［］表示，也可以创建制定类型的空数组。

    var emptyArray: Double[] = []
  
You can create multidimensional arrays by chaining multiple sets of square brackets to the name of the base type of the elements. For example, you can create a three-dimensional array of integers using three sets of square brackets:


<b>你可以链接多组中括号创建多维数组。</b>例如，你可以创建一个三维整数数组，通过三组中括号： 

    var array3D: Int[][][] = [[[1, 2], [3, 4]], [[5, 6], [7, 8]]]

When accessing the elements in a multidimensional array, the left-most subscript index refers to the element at that index in the outermost array. The next subscript index to the right refers to the element at that index in the array that’s nested one level in. And so on. This means that in the example above, array3D[0] refers to [[1, 2], [3, 4]], array3D[0][1] refers to [3, 4], and array3D[0][1][1] refers to the value 4.
   
当访问多维数组里面的元素时，最左边的下标指向最外层数组的对应位置，接下来往右的下标指向第一层嵌套的数组的位置。依此类推。根据上面的例子，array3D[0]指向[[1, 2], [3, 4]]，array3D[0][1]指向[3, 4]，array3D[0][1][1]的值是4。

For a detailed discussion of the Swift standard library Array type, see Arrays.

数组类型在swift标准库中的详细讨论，请看“数组“。


> GRAMMAR OF AN ARRAY TYPE

> 数组类型的语法
‌
> array-type → type[]  array-type[]

> 数组类型 → 类型[]  数组类型[] 
     
     
## Optional Type   
## 可选类型

The Swift language defines the postfix ? as syntactic sugar for the named type Optional<T>, which is defined in the Swift standard library. In other words, the following two declarations are equivalent:

在swift中定义后缀？为标准库定义的命名类型Optional<T>的简写。换句话说，以下两种声明是相等的：
    
    var optionalInteger: Int?
    var optionalInteger: Optional<Int>


In both cases, the variable optionalInteger is declared to have the type of an optional integer. Note that no whitespace may appear between the type and the ?.

在这两种情况下，变量optionalInteger被声明是可选整数类型。注意，在类型和？之间没有空格。

The type Optional<T> is an enumeration with two cases, None and Some(T), which are used to represent values that may or may not be present. Any type can be explicitly declared to be (or implicitly converted to) an optional type. When declaring an optional type, be sure to use parentheses to properly scope the ? operator. As an example, to declare an optional array of integers, write the type annotation as (Int[])?; writing Int[]? produces an error.

Optional<T> 是一个含有两种情况的枚举，None和Some(T)，用来表示可能有也可能没有值。任何类型都可以声明为（或者隐式转换）可选类型。当声明一个可选类型的时候，要确保用括号给？操作符提供确定的范围。例如，声明可选整数数组，应该写成(Int[])?；写成Int[]?会报错。

If you don’t provide an initial value when you declare an optional variable or property, its value automatically defaults to nil.

当你声明一个可选变量或者可选属性的时候没有提供初始值，它的值会默认设置为nil。

Optionals conform to the LogicValue protocol and therefore may occur in a Boolean context. In that context, if an instance of an optional type T? contains any value of type T (that is, it’s value is Optional.Some(T)), the optional type evaluates to true. Otherwise, it evaluates to false.

可选遵照LogicValue协议，因此可以出现在布尔环境中。在这种情况下，可选类型T?包含类型为T的任何值（也就是说它的值是Optional.Some(T)），这个可选类型等于true，反之为false。

If an instance of an optional type contains a value, you can access that value using the postfix operator !, as shown below:

如果可选类型包含一个值，你可以用后缀！访问，如下所示：

    optionalInteger = 42
    optionalInteger! // 42

Using the ! operator to unwrap an optional that has a value of nil results in a runtime error.

用操作符！去获取值为nil的可选变量回有运行错误。


You can also use optional chaining and optional binding to conditionally perform an operation on an optional expression. If the value is nil, no operation is performed and therefore no runtime error is produced.

你可以用可选链接和可选绑定选择性执行可选表达式上的操作。如果值为nil，任何操作都不会执行，也不会有运行报错。


For more information and to see examples that show how to use optional types, see Optionals.


更过关于可选类型的信息和例子，请看“可选“。

> GRAMMAR OF AN OPTIONAL TYPE

> 可选类型语法
 
> optional-type → type?

> 可选类型 → 类型 ?



## Implicitly Unwrapped Optional Type
## 隐式解析可选类型

The Swift language defines the postfix ! as syntactic sugar for the named type ImplicitlyUnwrappedOptional<T>, which is defined in the Swift standard library. In other words, the following two declarations are equivalent:


在swift中定义后缀！为标准库定义的名类型ImplicitlyUnwrappedOptional<T>的简写。换句话说，以下两种声明是相等的：

    var implicitlyUnwrappedString: String!
    var implicitlyUnwrappedString: ImplicitlyUnwrappedOptional<String>

In both cases, the variable implicitlyUnwrappedString is declared to have the type of an implicitly unwrapped optional string. Note that no whitespace may appear between the type and the !.

在这两种情况下，变量implicitlyUnwrappedString被声明为隐式可选类型字符串。注意，在类型和！之间没有空格。

You can use implicitly unwrapped optionals in all the same places in your code that you can use optionals. For instance, you can assign values of implicitly unwrapped optionals to variables, constants, and properties of optionals, and vice versa.

你代码中用到可选的地方都可以用隐式解析可选。例如，你可以设置隐式可选类型的值为变量、常量、可选属性，反之亦然。

As with optionals, if you don’t provide an initial value when you declare an implicitly unwrapped optional variable or property, it’s value automatically defaults to nil.

有了可选，当你声明一个隐式解析可选变量或者属性的时候没有赋初始值，它的值默认为nil。


Because the value of an implicitly unwrapped optional is automatically unwrapped when you use it, there’s no need to use the ! operator to unwrap it. That said, if you try to use an implicitly unwrapped optional that has a value of nil, you’ll get a runtime error.

隐式解析可选的值会在使用的时候自动解析，所以不需要用！去解析它。也就是说，如果你用值为nil的隐式解析可选，那么会会导致运行错误。

Use optional chaining to conditionally perform an operation on an implicitly unwrapped optional expression. If the value is nil, no operation is performed and therefore no runtime error is produced.

使用可选链能够选择性的执行隐式解析可选表达式上的操作。用可选链接在隐式解析可选的表达式上做一定的操作。如果值是nil，没有操作会被执行，也不会有运行错误。

For more information about implicitly unwrapped optional types, see Implicitly Unwrapped Optionals.

更多关于隐式解析可选类型，请看 “隐式解析可选”。

> GRAMMAR OF AN IMPLICITLY UNWRAPPED OPTIONAL TYPE

> 隐式解析可选类型语法

> implicitly-unwrapped-optional-type → type!

> 隐式解析可选类型 -> 类型！



## Protocol Composition Type
## 协议组合类型

A protocol composition type describes a type that conforms to each protocol in a list of specified protocols. Protocol composition types may be used in type annotations and in generic parameters.

协议组合类型是指符合指定协议列表里每个协议的类型。协议组合类型可以用在类型注释和泛型参数中。


Protocol composition types have the following form:

协议组合类型的格式如下：

    protocol<Protocol 1, Protocol 2> 

A protocol composition type allows you to specify a value whose type conforms to the requirements of multiple protocols without having to explicitly define a new, named protocol that inherits from each protocol you want the type to conform to. For example, specifying a protocol composition type protocol<ProtocolA, ProtocolB, ProtocolC> is effectively the same as defining a new protocol ProtocolD that inherits from ProtocolA, ProtocolB, and ProtocolC, but without having to introduce a new name.

<b>它的类型符合多个协议的要求，不需定义新的命名协议，它继承了从每个协议符合的类型。</b>。例如，指定一个协议组合类型protocol<ProtocolA, ProtocolB, ProtocolC>相当于定义一个新的协议ProtocolD，它继承了ProtocolA, ProtocolB和 ProtocolC，但是没有引入一个新的名字。

Each item in a protocol composition list must be either the name of protocol or a type alias of a protocol composition type. If the list is empty, it specifies the empty protocol composition type, which every type conforms to.

协议组合列表中的每一项必须是协议名或者是协议组合类型的别名。如果列表是空的，它会指定一个空的协议组合类型，任何类型都可以匹配。


> GRAMMAR OF A PROTOCOL COMPOSITION TYPE
> 
> 协议组合类型语法

> protocol-composition-type → protocol<protocol-identifier-list[opt]>
> 
> 协议组合类型 -> 协议<协议标示符列表［可选］>

> protocol-identifier-list → protocol-identifier ｜ protocol-identifier,protocol-identifier-list

> 协议标示符列表 -> 协议标示符 ｜ 协议标示符，协议标示符列表
> 
> protocol-identifier → type-identifier 

> 协议标示符 -> 类型标示符


## Metatype Type
## 元类型

A metatype type refers to the type of any type, including class types, structure types, enumeration types, and protocol types.

元类型是指所有类型的类型，包括类、结构、枚举、协议。

The metatype of a class, structure, or enumeration type is the name of that type followed by .Type. The metatype of a protocol type—not the concrete type that conforms to the protocol at runtime—is the name of that protocol followed by .Protocol. For example, the metatype of the class type SomeClass is SomeClass.Type and the metatype of the protocol SomeProtocol is SomeProtocol.Protocol.


类、结构、枚举的元类型是相应的类型名称后面跟着.Type。协议类型的元类型 -- 不是具体的类型，根据协议运行时来适配 -- 是该协议名字后面跟着.Protocol。例如，类SomeClass的元类型是SomeClass.Type，协议SomeProtocol的元类型是SomeProtocol.Protocol。

You can use the postfix self expression to access a type as a value. For example, SomeClass.self returns SomeClass itself, not an instance of SomeClass. And SomeProtocol.self returns SomeProtocol itself, not an instance of a type that conforms to SomeProtocol at runtime. You can use a dynamicType expression with an instance of a type to access that instance’s runtime type as a value, as the following example shows:


你可以用后缀self的方式获取类型。例如，SomeClass.self返回 SomeClass本身，不是SomeClass的实例。SomeProtocol.self返回SomeProtocol本身, 不是运行时SomeProtocol的实例。你可以用dynamicType表达式类获取实例运行时的类型，如下面的例子所示：

    class SomeBaseClass {
        class func printClassName() {
            println("SomeBaseClass")
        }
    }
    class SomeSubClass:SomeBaseClass {
        override class func printClassName() {
            println("SomeSubClass")
        }
    }
    let someInstance: SomeBaseClass = SomeSubClass()
    // someInstance is of type SomeBaseClass at compile time, but
    // someInstance is of type SomeSubClass at runtime
    
    someInstance.dynamicType.printClassName()
       
    // prints "SomeSubClass"
    

> GRAMMAR OF A METATYPE TYPE

> 元类型语法

> metatype-type → type.Type ｜ type.Protocol

> 元类型 → 类型.Type ｜ 类型.Protocol
> 

## Type Inheritance Clause
## 类型继承子句

A type inheritance clause is used to specify which class a named type inherits from and which protocols a named type conforms to. A type inheritance clause begins with a colon (:), followed by a comma-separated list of type identifiers.

类型继承子句被用来指定一个命名类型继承哪个类，适配哪些协议。类型继承子句以冒号（：）开始，紧跟着以逗号分割的类型标示符列表。


Class types may inherit from a single superclass and conform to any number of protocols. When defining a class, the name of the superclass must appear first in the list of type identifiers, followed by any number of protocols the class must conform to. If the class does not inherit from another class, the list may begin with a protocol instead. For an extended discussion and several examples of class inheritance, see Inheritance.

类类型可能继承单个超类，适配多个协议。当定义一个类的时候，超类的名称必须出现在类型标示符列表首位，接着类必须适配的一些协议。如果类不继承其他类，那么列表就是以协议开头。类机继承的扩展讨论和例子，请看 “继承”。


Other named types may only inherit from or conform to a list of protocols. Protocol types may inherit from any number of other protocols. When a protocol type inherits from other protocols, the set of requirements from those other protocols are aggregated together, and any type that inherits from the current protocol must conform to all of those requirements.

其他命名协议可能仅继承或适配一个协议列表。协议类型可能继承一些其它协议。当一个协议类型继承其它协议的时候，其它协议的条件会被集合在一起，任何继承当前协议的类型必须适配所有的这些条件。

A type inheritance clause in an enumeration definition may be either a list of protocols, or in the case of an enumeration that assigns raw values to its cases, a single, named type that specifies the type of those raw values. For an example of an enumeration definition that uses a type inheritance clause to specify the type of its raw values, see Raw Values.


<b>在枚举类型里面定义的类型继承子句可以是一个协议列表，或者指定原始值的枚举实例，一个单独的指定原始值类型的命名型类型。</b>在枚举定义中用类型继承子句来指定原始值类型的列子，请看 “原始类型”。

> GRAMMAR OF A TYPE INHERITANCE CLAUSE

> 类型继承子句语法
    
> type-inheritance-clause → :type-inheritance-list
> 
> 类型继承子句 → : 类型继承列表
> 
> type-inheritance-list → type-identifier ｜ type-identifier,type-inheritance-list

> 类型继承列表 → 类型标示符 ｜ 类型表示符，类型继承列表


## Type Inference 
## 类型推断

Swift uses type inference extensively, allowing you to omit the type or part of the type of many variables and expressions in your code. For example, instead of writing var x: Int = 0, you can omit the type completely and simply write var x = 0—the compiler correctly infers that x names a value of type Int. Similarly, you can omit part of a type when the full type can be inferred from context. For instance, if you write let dict: Dictionary = ["A": 1], the compiler infers that dict has the type Dictionary<String, Int>.


swift广泛使用类型推断，允许你在代码里忽略很多变量和表达式的类型或者部分类型。例如，var x: Int = 0可以完全忽略类型，简写成 var x ＝ 0 -- 编译器能够正确的推测出x的类型名称是Int。同样，当完整的类型能够通过上下文推断出来的时候，你可以忽略部分类型。例如，
dict: Dictionary = ["A": 1],编译器推断出dict的类型是Dictionary<String, Int>。

In both of the examples above, the type information is passed up from the leaves of the expression tree to its root. That is, the type of x in var x: Int = 0 is inferred by first checking the type of 0 and then passing this type information up to the root (the variable x).


在上面的两个例子中，类型信息从表达树的叶子传向根。也就是说，x在var x: Int = 0的类型通过首先判断0的类型，然后再传递类型信息到根（即变量x）。


In Swift, type information can also flow in the opposite direction—from the root down to the leaves. In the following example, for instance, the explicit type annotation (: Float) on the constant eFloat causes the numeric literal 2.71828 to have type Float instead of type Double.

在swift里面，类型推断可以反方向推断 -- 从根传递到叶子。下面这个例子就是这种情况，常量eFloat显示类型注释（：Float）导致数字2.71828的类型是Float而不是Double。

    let e = 2.71828 // The type of e is inferred to be Double.
    let eFloat: Float = 2.71828 // The type of eFloat is Float.


Type inference in Swift operates at the level of a single expression or statement. This means that all of the information needed to infer an omitted type or part of a type in an expression must be accessible from type-checking the expression or one of its subexpressions.

swift中的类型推断在单个表达式或者语句上操作。这意味着推测忽略类型或者部分类型信息必须从表达式或者其子表达式类型检测中获取。

























