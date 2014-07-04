# 类型
在swift里，有两种类型：命名类型和复合类型。命名类型是指在定义的时候能够给一个指定名字的类型。命名类型包含类、结构、枚举和协议。例如，一个用户自定义的名为MyClass的类的实例，其类型就是MyClass。除了用户定义的命名类型，swift标准库还定义了很多常用命名类型，如一些数组，字典，可选值。

一些被其它语言视为是最基础或最原始的数据类型，例如数字、字符、字符串，实际上都是命名类型，swift标准库使用结构去定义和实现他们。由于他们是命名类型的，你可以用扩展声明来扩展他们的功能，来满足你的程序需求，具体请参考 “扩展和扩展声明“。

复合类型是一个没有名字的类型，由swift内部自己定义。swift有两种复合类型：函数类型和元组类型。一个复合数据类型可以包含命名类型和其他复合类型。例如，一个元组类型（Int, (Int, Int)）包含两个元素：第一个的命名类型是Int，第二个是其他复合类型（Int, Int）。

本章讨论swift语言本身定义的类型，并描述在swift中类型推断的方式。

> 类型的语法

> 类型 -> 数组类型｜函数类型｜类型标识｜元组类型｜可选类型｜隐式去包装可选类型｜协议构成类型｜元型类型


## 类型注解


类型注解明确的指定一个变量或者表达式的类型。类型注解以冒号(:)开始，以类型结束，如下面的例子：
    
    1. let someTuple:(Double, Double) = (3.14159, 2.71828)

    2. func someFunction(a:Int) { /**/}
    
在第一个例子中，表达式someTuple是被定义为元组类型(Double, Double)。在第二个例子中，函数someFuncion中的参数a被定义为Int类型。


类型注解可以在类型前面包含一个可选的类型属性的列表。

> 类型注解的语法

> 类型注解 -> :属性［可选］类型


## 类型标识符


类型标识符是指一个命名类型或者命名类型/复合类型的别名。


大多数情况下，类型标识符直接指向和标示符命名相同的命名类型。例如，类型标识符Int指向命名类型Int，类型标识符Dictionary指向命名类型Dictionary。


命名标识符和类型标识符不同名有两种情况。第一种情况，命名标识符指向命名类型或者复合类型的别名。例如，在下面的例子中，类型标识符使用Point指向元组类型(Int, Int)。

    typealias Point = (Int, Int);
    let origin: Point = (0, 0);

第二种情况，类型标识符用点（.）指向在其它模块中声明或嵌套在其它类型中的命名类型。例如，在下面的代码中，类型标识符引用在模块ExampleModule中声明的命名类型MyType。
    
    var someValue: ExampleModule.MyType   
     

> 命名标识符的语法

> 命名标识符 -> 类型名称 泛型参数子句［可选］｜类型名称 泛型参数子句［可选］.类型标识符

> 类型标识符 -> 标识符


## 元组类型

元组类型是指在括号中，用逗号分隔的零到多个类型的列表。


你可以用元组类型作为函数的返回值类型，这样函数就能返回包含多个值的单元组。你也可以给元组类型中的元素命名，用这些名字来指代单个元素的值。元素的名字由标识符和紧跟着的冒号(:)组成。关于这两种特性的具体用法，请看 “多个返回值的函数“。

Void是空元组类型的别名，表示为()。如果在括号里面只有一个元素，那么这个类型就是这个元素的类型。例如，(Int)的类型是Int，不是(Int)。因此，你可以认为仅当元组类型包含两个或者更多元素的时候才是元组元素。


> 元组类型的语法


> 元组类型 -> (元组类型体［可选］)


> 元组类型体 -> 元组类型元素列表...［可选］


> 元组类型元素列表 -> 元组类型元素｜元组类型元素，元组类型元素列表


> 元组类型元素 -> 属性［可选］inout［可选］类型｜inout［可选］元素名称 类型注解


> 元素名称 -> 标识符


## 函数类型


函数类型表示一个函数，方法或者闭包的类型，它由参数和返回类型组成，中间通过箭头(->)分隔：
   
由于参数类型和返回类型都可以为元组类型，所以函数类型支持含有多个参数和多个返回值的函数和方法。

你可以把自动闭包（auto_closure）的属性归为有一个参数类型为()，返回值为表达式类型(请看 “类型属性“)的函数类型。一个自动闭包函数捕获的是指定表达式上的隐式闭包而不是表达式本身。下面的例子用auto_closure属性来定义一个简单的assert函数：
    
    func simpleAssert(condition: @auto_closure () -> Bool, message: String){
        if !condition(){
            println(message)
        }
    }
    let testNumber = 5
    simpleAssert(testNumber % 2 == 0, "testNumber isn't an even number.")
    // prints "testNumber isn't an even number."
    


一个函数类型在参数类型中可以让一个可变参数作为其最后一个参数。从语法上来说，可变参数可以由一个基础类型名称和紧跟着的三个点(...)组成，例如Int...。可变参数被认为是一个包含基础类型名称的数组。例如，可变参数Int... 被认为是Int[]。使用可变参数的例子，请参考 “可变参数“。


指定一个in-out参数，需要给参数类型加上inout的前缀。可变参数和返回类型不能使用inout标记。in-out参数在’In-Out参数‘中有讨论。


柯里化函数（curried function）类型相当于嵌套函数类型。例如，下面的柯里化函数addTwoNumbers()()的类型是Int -> Int -> Int:

    func addTwoNumbers(a: Int)(b: Int) -> Int{
        return a + b
    }

    addTwoNumbers(4)(5)      // returns 9


柯里化函数的函数类型从右到左形成一组。例如，函数类型Int -> Int -> Int被理解为Int -> (Int -> Int) -- 指函数传入一个Int，然后返回另外一个输入输出都是Int的函数。例如，你可以把柯里化函数addTwoNumbers()()写成如下的嵌套函数形式：
     
     func addTwoNumbers(a: Int) -> (Int -> Int){
        func addTheSecondNumber(b: Int) -> Int{
            return a + b
        }
        return addTheSecondNumber
    }

    addTwoNumbers(4)(5)     // Returns 9


> 函数类型的语法

> 函数类型 → 类型 -> 类型


## 数组类型


在swift中类型紧跟着可括号[]作为标准库定义的命名类型Array的简写。换句话说，下面两个声明是相等的：

    let someArray: String[] = ["Alex", "Brian", "Dave"]
    let someArray: Array<String> = ["Alex", "Brian", "Dave"]


在这两种情况下，常量someArray被定义为字符串数组。数组元素也可以用中括号访问：someArray[0] 指向index为0的元素，即‘Alex’。

如上所示，你可以用数组自变量字面量？和[]创建一个数组。空数组自变量用[]表示，也可以创建特定类型的空数组。

    var emptyArray: Double[] = []


你可以用多组中括号相连来创建多维数组。例如，你可以用三组中括号来创建一个三维整数数组：

    var array3D: Int[][][] = [[[1, 2], [3, 4]], [[5, 6], [7, 8]]]


当访问多维数组里面的元素时，最左边的下标指向数组最外层对应位置的元素，接下来往右的下标指向第一层嵌套的数组相应位置的元素。依此类推。根据上面的定义，则array3D[0]指向[[1, 2], [3, 4]]，array3D[0][1]指向[3, 4]，array3D[0][1][1]的值是4。


想要更多了解swift标准库中关于数组类型的详细讨论，请看 “数组“。

> 数组类型的语法

> 数组类型 → 类型[] 数组类型[]


## 可选类型


Swfit语言定义后缀？作为命名类型Optional的简写，换句话说，以下两种声明是相等的：

    var optionalInteger: Int?
    var optionalInteger: Optional<Int>

在这两种情况下，变量optionalInteger都是可选整数类型。注意，在类型和？之间没有空格。


Optional 是一个含有两种情况的枚举，None和Some(T)，用来表示可能有或可能没有值。任何类型都可以明确声明为（或者隐式转换）可选类型。当声明一个可选类型的时候，要确保用括号给？操作符一个合适的范围。例如，声明可选整数数组，应该写成(Int[])?；写成Int[]?会报错。


当你声明一个可选变量或者可选属性的时候没有提供初始值，它的值会默认为nil。


可选项遵照LogicValue协议，因此可以出现在布尔环境中。在这种情况下，如果可选类型T?包含类型为T的任何值（也就是说它的值是Optional.Some(T)），这个可选类型等于true，反之为false。


如果一个可选类型的实例包含一个值，你可以用后缀操作符！来访问这个值，如下所示：

    optionalInteger = 42
    optionalInteger! // 42

使用操作符！去获取值为nil的可选变量会有运行时错误。


你可以用可选链接和可选绑定选择性执行可选表达式上的操作。如果值为nil，任何操作都不会执行，也不会有运行报错。


更过关于可选类型的信息和例子，请看 “可选“。


> 可选类型语法


> 可选类型 → 类型 ?



## 隐式解析可选类型

在swift中定义后缀！为标准库定义的名类型ImplicitlyUnwrappedOptional的简写。换句话说，以下两种声明是相等的：

    var implicitlyUnwrappedString: String!
    var implicitlyUnwrappedString: ImplicitlyUnwrappedOptional<String>


在这两种情况下，变量implicitlyUnwrappedString被声明为隐式可选类型字符串。注意，在类型和！之间没有空格。


你代码中用到可选的地方都可以用隐式解析可选。例如，你可以设置隐式可选类型的值为变量、常量、可选属性，反之亦然。


有了可选，当你声明一个隐式解析可选变量或者属性的时候没有赋初始值，它的值默认为nil。


隐式解析可选的值会在使用的时候自动解析，所以不需要用！去解析它。也就是说，如果你用值为nil的隐式解析可选，那么将会导致运行错误。


使用可选链能够选择性的执行隐式解析可选表达式上的操作。用可选链接在隐式解析可选的表达式上做一定的操作。如果值是nil，没有操作会被执行，也不会有运行错误。

更多关于隐式解析可选类型，请看 “隐式解析可选”。


> 隐式解析可选类型语法

> 隐式解析可选类型 -> 类型！


## 协议组合类型

协议组合类型是指符合指定协议列表里每个协议的类型。协议组合类型可以用在类型注解和泛型参数中。

协议组合类型的格式如下：

    protocol<Protocol 1, Protocol 2> 

一个协议组合类型的类型符合多个协议的要求，不需定义新的命名协议，它继承了从每个协议符合的类型。例如，指定一个协议组合类型protocol相当于定义一个新的协议ProtocolD，它继承了ProtocolA，ProtocolB和 ProtocolC，但是没有引入一个新的名字。

协议组合列表中的每一项必须是协议名或者是协议组合类型的别名。如果列表是空的，它会指定一个空的协议组合类型，任何类型都可以匹配。


> 协议组合类型语法

> 协议组合类型 -> 协议<协议标示符列表［可选］>

> 协议标示符列表 -> 协议标示符 ｜ 协议标示符，协议标示符列表

> 协议标示符 -> 类型标示符


## 元类型


元类型是指所有类型的类型，包括类、结构、枚举、协议。


类、结构、枚举的元类型是相应的类型名称后面跟着的名字.Type。协议类型的元类型 -- 不是具体的类型，而是根据协议运行时来适配 -- 是该协议后面跟着的名字.Protocol。例如，类SomeClass的元类型是SomeClass.Type，协议SomeProtocol的元类型是SomeProtocol.Protocol。


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


> 元类型语法

> 元类型 → 类型.Type ｜ 类型.Protocol



## 类型继承子句


类型继承子句被用来指定一个命名类型继承哪个类，适配哪些协议。类型继承子句以冒号(:)开始，紧跟着以逗号分割的类型标示符列表。


类类型可能继承单个超类，适配多个协议。当定义一个类的时候，超类的名称必须出现在类型标示符列表首位，接着是类必须适配的一些协议。如果类不继承其他类，那么列表就是以协议开头。类机继承的扩展讨论和例子，请看 “继承”。


其他命名协议可能仅继承或适配一个协议列表。协议类型可能继承多个其它协议。当一个协议类型继承其它协议的时候，其它协议的条件会被集合在一起，任何继承当前协议的类型必须适配所有的这些条件。


在枚举类型里面定义的类型继承子句可以是一个协议列表，或者指定原始值的枚举实例，或一个单独的指定原始值类型的命名型类型。在枚举定义中用类型继承子句来指定原始值类型的例子，请看 “原始类型”。


> 类型继承子句语法

> 类型继承子句 → : 类型继承列表

> 类型继承列表 → 类型标示符 ｜ 类型表示符，类型继承列表



## 类型推断


swift广泛使用类型推断，它允许你在代码里忽略很多变量和表达式的类型或者部分类型。例如，var x: Int = 0可以完全忽略类型，简写成 var x ＝ 0 -- 编译器能够正确的推测出x的类型名称是Int。同样，当完整的类型能够通过上下文推断出来的时候，你可以忽略部分类型。例如， dict: Dictionary = ["A": 1]，编译器推断出dict的类型是Dictionary。


在上面的两个例子中，类型信息从表达树的叶子传向根。也就是说，x在var x: Int = 0的类型通过首先判断0的类型，然后再传递类型信息到根（即变量x）。


在swift里面，类型推断可以反方向推断 -- 从根传递到叶子。下面这个例子就是这种情况，常量eFloat显示类型注解（：Float）导致数字2.71828的类型是Float而不是Double。

    let e = 2.71828 // The type of e is inferred to be Double.
    let eFloat: Float = 2.71828 // The type of eFloat is Float.
    
swift中的类型推断在单个表达式或者语句上操作。这意味着推测忽略类型或者部分类型信息必须从表达式或者其子表达式类型检测中获取。

