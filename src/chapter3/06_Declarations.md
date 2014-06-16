# 声明
A declaration introduces a new name or construct into your program. For example, you use declarations to introduce functions and methods, variables and constants, and to define new, named enumeration, structure, class, and protocol types. You can also use a declaration to extend the the behavior of an existing named type and to import symbols into your program that are declared elsewhere.

声明将新的名字或者结构引入到程序中。例如，使用声明可以引入函数、方法、变量和常量；可以定义新的，命名的枚举类型，接口，类和原型类型。也可以使用声明来扩展已存在命名类型的行为，在程序中引入在其它地方声明的符号。

In Swift, most declarations are also definitions in the sense that they are implemented or initialized at the same time they are declared. That said, because protocols don’t implement their members, most protocol members are declarations only. For convenience and because the distinction isn’t that important in Swift, the term declaration covers both declarations and definitions.

在Swift中，大多数声明在某种意义上也是定义，可以在声明的同时实现和初始化他们。。也就是说，因为协议不会实现他们的成员，大多数协议成员仅仅是声明。为了方便，因为这个不同在Swift里不是那么重要，因此这个术语declaration同时包含了声明和定义。

>GRAMMAR OF A DECLARATION

>declaration → import-declaration­

>declaration → constant-declaration­

>declaration → variable-declaration­

>declaration → typealias-declaration­

>declaration → function-declaration­

>declaration → enum-declaration­

>declaration → struct-declaration­

>declaration → class-declaration­

>declaration → protocol-declaration­

> declaration → initializer-declaration­

>declaration → deinitializer-declaration­

> declaration → extension-declaration­

> declaration → subscript-declaration­

>declaration → operator-declaration­

>declarations → declaration­declarations­opt­

>declaration-specifiers → declaration-specifier­declaration-specifiers­opt­

>declaration-specifier → class­ | mutating ­| nonmutating­ | override­ | static­ | unowned 

## 模块范围

The module scope defines the code that’s visible to other code in Swift source files that are part of the same module. The top-level code in a Swift source file consists of zero or more statements, declarations, and expressions. Variables, constants, and other named declarations that are declared at the top-level of a source file are visible to code in every source file that is part of the same module。

>GRAMMAR OF A TOP-LEVEL DECLARATION

>top-level-declaration → statements­opt

Code Blocks

代码块

A code block is used by a variety of declarations and control structures to group statements together. It has the following form:

大量不同的声明和控制结构通过代码块来把语句分组。有如下的形式：

    {
        `statements`
    }
    
The statements inside a code block include declarations, expressions, and other kinds of statements and are executed in order of their appearance in source code.

在代码块里的语句包括声明，表达式，和其它类型的语句，按照在源代码里出现的顺序只习惯。

>GRAMMAR OF A CODE BLOCK
>code-block → {­statements­opt­}

##Import Declaration

## Import 声明

An import declaration lets you access symbols that are declared outside the current file. The basic form imports the entire module; it consists of the import keyword followed by a module name:


import声明可以让你访问到当前文件之外的符号。基本的形式是引入整个模块。由import关键字后面跟着一个模块名。


  import module
 
Providing more detail limits which symbols are imported—you can specify a specific submodule or a specific declaration within a module or submodule. When this detailed form is used, only the imported symbol (and not the module that declares it) is made available in the current scope.

如果提供更多的细节，你还可以明确限制引入一个具体的子模块或者子模块里的一个具体的声明。如果采用这种形式的声明，只有被引入的符号（而不是声明它的模块）可以在当前范围里访问到。

  import import kind module.symbol name
  import module.submodule

>GRAMMAR OF AN IMPORT DECLARATION

>import-declaration → attributes ­opt ­import­ import-kind­ opt import-path­
>import-kind → typealias­ | struct­ | class­ | enum­ | protocol­ | var­ | func­
>import-path → import-path-identifier­  import-path-identifier­.­import-path­
>import-path-identifier → identifier­  operator

##Constant Declaration

##常量声明

A constant declaration introduces a constant named value into your program. Constant declarations are declared using the keyword let and have the following form:

常量声明会在你的程序里引入一个不变的命名值。常量声明使用关键字let，采用如下的形式：

  let constant name: type = expression

A constant declaration defines an immutable binding between the constant name and the value of the initializer expression; after the value of a constant is set, it cannot be changed. That said, if a constant is initialized with a class object, the object itself can change, but the binding between the constant name and the object it refers to can’t.

常量声明在常量名和初始化表达式的值之间定义了一个不可变的绑定；在值被设置之后，它就不能改变了。也就是说，如果常量用一个class对象实例化，对象本身可以改变，但是在常量名和对象之间的绑定时不会改变的。

When a constant is declared at global scope, it must be initialized with a value. When a constant declaration occurs in the context of a class or structure declaration, it is considered a constant property. Constant declarations are not computed properties and therefore do not have getters or setters.

如果一个常量在全局范围里声明，它就必须有一个初始值。当一个常量在类或者结构声明中声明的，它会被认为是一个常量属性。常量声明不是i可计算的属性，因此没有getters和setters方法。

If the constant name of a constant declaration is a tuple pattern, the name of each item in the tuple is bound to the corresponding value in the initializer expression.

如果一个常量的声明的名字是一个元组模式，在元组中的没一项在初始化表达式里都会绑定到响应的值。

  let (firstNumber, secondNumber) = (10, 42)
  
In this example, firstNumber is a named constant for the value 10, and secondNumber is a named constant for the value 42. Both constants can now be used independently:

在这个例子，firstNumer是一个命令常量，值是10.secondNumber是一个命令的常量，值是42.这两个常量现在都可以独立的使用。

    1  println("The first number is \(firstNumber).")
    2  // prints "The first number is 10."
    3  println("The second number is \(secondNumber).")
    4  // prints "The second number is 42."
    
The type annotation (: type) is optional in a constant declaration when the type of the constant name can be inferred, as described in Type Inference.

在常量声明中，如果常量名的类型可以被推断出来，type是可选的，正如在Type Inference里描述的。

To declare a static constant property, mark the declaration with the static keyword. Static properties are discussed in Type Properties.

为了声明一个静态的常量属性，使用static关键字 来标记声明。静态属性在TypeProerties里讨论。

For more information about constants and for guidance about when to use them, see Constants and Variables and Stored Properties
想获得更多关于常量的信息或者想在使用中获得帮助，请查看常量和变量和存储属性（stored properties）等节。

>GRAMMAR OF A CONSTANT DECLARATION

>constant-declaration → attributes­ opt ­declaration-specifiers­ opt ­let­pattern-initializer-list­
>pattern-initializer-list → pattern-initializer­ | pattern-initializer­ , pattern-initializer-list­
>pattern-initializer → pattern ­initializer ­opt­
>initializer → =­expression


##Variable Declaration

##变量声明

A variable declaration introduces a variable named value into your program and is declared using the keyword var.

变量声明会引入一个可变的命令值到你的程序中，使用关键字var进行声明。

Variable declarations have several forms that declare different kinds of named, mutable values, including stored and computed variables and properties, stored variable and property observers, and static variable properties. The appropriate form to use depends on the scope at which the variable is declared and the kind of variable you intend to declare.

变量声明有好几种不同的形式来声明命令的，可变的值，包括可存储的可计算的变量和属性，可存储的变量和属性观察者。还有静态的变量属性。要使用哪种具体的形式取决于变量声明的范围和你打算声明的变量种类。

>注意：
>你也可以在协议声明的上下文声明属性，详情参见类型属性声明。

You can override a property in a subclass by prefixing the subclass’s property declaration with the override keyword, as described in Overriding.

你可以在子类中重写一个属性通过在子类中的属性声明的前面使用override。


##Stored Variables and Stored Variable Properties

##存储型变量和存储型变量属性

The following form declares a stored variable or stored variable property:

下面的形式声明了一可存储的变量或可存储的变量属性

 var variable name: type = expression
 
You define this form of a variable declaration at global scope, the local scope of a function, or in the context of a class or structure declaration. When a variable declaration of this form is declared at global scope or the local scope of a function, it is referred to as a stored variable. When it is declared in the context of a class or structure declaration, it is referred to as a stored variable property.

你可以在全局范围、函数的局部范围或者类或结构声明的环境里定义变量声明。如果这种形式的变量声明在全局或者函数局部范围里声明，它指的就是可存储的变量。如果是在类或者结构声明的环境里声明的，它就是指的可存储变量属性。

The initializer expression can’t be present in a protocol declaration, but in all other contexts, the initializer expression is optional. That said, if no initializer expression is present, the variable declaration must include an explicit type annotation (: type).

初始化表达式不能在协议声明里出现，但是可以出现在其它所有的环境里。初始化表达式是可选的。也就是说，如果没有初始化表达式存在，变量声明必须包括一个现实的类型表示。

As with constant declarations, if the variable name is a tuple pattern, the name of each item in the tuple is bound to the corresponding value in the initializer expression.

和常量声明一样，如果变量名字是一个元组模式，元组中每一项的名字都会被绑定到初始化表达式的对应的值里


As their names suggest, the value of a stored variable or a stored variable property is stored in memory.

顾名思义，存储变量的或者存储属性的值是存储在内存中的。

##Computed Variables and Computed Properties

##计算型变量和计算型属性

The following form declares a computed variable or computed property:

下面的形式声明了一个可计算的变量或者可计算的属性

  var variable name: type {
  get {
    statements
  }
  set(setter name) {
    statements
  }
  }
You define this form of a variable declaration at global scope, the local scope of a function, or in the context of a class, structure, enumeration, or extension declaration. When a variable declaration of this form is declared at global scope or the local scope of a function, it is referred to as a computed variable. When it is declared in the context of a class, structure, or extension declaration, it is referred to as a computed property.

可以在全局范围，局部范围，或者类、结构、枚举或者可扩展的声明。如果这类型是的变量声明在全局或者函数的局部返回声明，指的是可计算的变量。如果它在一个雷，结构或者扩展声明里，它就是指的可计算的属性。


The getter is used to read the value, and the setter is used to write the value. The setter clause is optional, and when only a getter is needed, you can omit both clauses and simply return the requested value directly, as described in Read-Only Computed Properties. But if you provide a setter clause, you must also provide a getter clause.

getter用于读取值，setter用于写入值。setter语句是可选的，仅仅getter方法是需要的，你可以把两者都忽略，只是简单的返回请求的值，正如在Read-Only Comuted Properties.但是如果你提供一个setter y语句，你不想页提供一个getter语句。

The setter name and enclosing parentheses is optional. If you provide a setter name, it is used as the name of the parameter to the setter. If you do not provide a setter name, the default parameter name to the setter is newValue, as described in Shorthand Setter Declaration.

setter名字和封闭的大括号是可选的。如果你i供一个setter名字。如果你提供一个setter名字，它会被作为setter的参数的名称。如果你不提供setter名称，setter缺省的参数名是newvalue,正如在Shorthand Setter Declaration.

Unlike stored named values and stored variable properties, the value of a computed named value or a computed property is not stored in memory.

不像存储的名字值和存储的变量属性，可计算名字的值或者计算属性的值不会存储到内存中。

For more information and to see examples of computed properties, see Computed Properties.

获得更多信息，查看如何使用属性监视器的例子，请查看属性监视器(prpperty observers)一节。

##Stored Variable Observers and Property Observers

##存储型变量监视器和属性监视器

You can also declare a stored variable or property with willSet and didSet observers. A stored variable or property declared with observers has the following form:

你也可以声明一个存储变量或者属性使用willset和didset 观察者。一个存储变量或者声明的属性有以下的形式：

var variable name: type = expression {
willSet(setter name) {
    statements
}
didSet(setter name {
    statements
}
}

You define this form of a variable declaration at global scope, the local scope of a function, or in the context of a class or structure declaration. When a variable declaration of this form is declared at global scope or the local scope of a function, the observers are referred to as stored variable observers. When it is declared in the context of a class or structure declaration, the observers are referred to as property observers.

你可以i在全局范围，函数的局部返回，或者类，结构环境里声明这种形式的变量。当这类型是的变量声明在全局范围或者函数的局部范围里声明的时候，观察者会被作为可存储的变量观察者。当在类或者结构声明中声明的时候，观察者会被作为属性的观察者。

You can add property observers to any stored property. You can also add property observers to any inherited property (whether stored or computed) by overriding the property within a subclass, as described in Overriding Property Observers.

可以为任何存储属性增加观察器。你可以可以为继承的属性增加属性观察器（无论是存储的或是计算的）通过使用子类覆盖，就像Overriding PropertyOververs里描述的一样。

The initializer expression is optional in the context of a class or structure declaration, but required elsewhere. The type annotation is required in all variable declarations that include observers, regardless of the context in which they are declared.

在类或者结构声明里，初始化表达式是可选的。但是在其他所有地方时必须的。类型保险在所有变量声明里是必须的，包括观测器，无论他们声明的环境。

The willSet and didSet observers provide a way to observe (and to respond appropriately) when the value of a variable or property is being set. The observers are not called when the variable or property is first initialized. Instead, they are called only when the value is set outside of an initialization context.

willset 和 didset 观察器提供了方式来观察好合适的响应在一个变量或者属性的值被设置的时候。观察器仅仅在初始化环境的外边可以被调用。

A willSet observer is called just before the value of the variable or property is set. The new value is passed to the willSet observer as a constant, and therefore it can’t be changed in the implementation of the willSet clause. The didSet observer is called immediately after the new value is set. In contrast to the willSet observer, the old value of the variable or property is passed to the didSet observer in case you still need access to it. That said, if you assign a value to a variable or property within its own didSet observer clause, that new value that you assign will replace the one that was just set and passed to the willSet observer.

willset观察器只是在变量或是属性被设置的时候被调用。新值会被作为常量传递给willset语句。didSet观察期在新值被设置的时候被调用。与willset相比，变量或属性的旧值。

The setter name and enclosing parentheses in the willSet and didSet clauses are optional. If you provide setter names, they are used as the parameter names to the willSet and didSet observers. If you do not provide setter names, the default parameter name to the willSet observer is newValue and the default parameter name to the didSet observer is oldValue.

在willset和didset语句里 setter名字和括号是可选的。如果你提供你不提供setter名字，willset 缺省的参数名是newValue好缺省的参数名是oldValue.

The didSet clause is optional when you provide a willSet clause. Likewise, the willSet clause is optional when you provide a didSet clause.

如果你提供一个willset语句，didset语句是可选的。同样的，如果你提供一个didset 语句，willset语句是可选的

For more information and to see an example of how to use property observers, see Property Observers.

获得更多信息，查看如何使用属性监视器的例子，请查看属性监视器(prpperty observers)一节。

##Class and Static Variable Properties

##类和静态变量属性

To declare a class computed property, mark the declaration with the class keyword. To declare a static variable property, mark the declaration with the static keyword. Class and static properties are discussed in Type Properties.
要声明一个类计算属性，要用class关键字标记声明。声明静态的变量属性，用关键字static标记声明。类和静态属性在Type属性里讨论。

>GRAMMAR OF A VARIABLE DECLARATION

>variable-declaration → variable-declaration-head­pattern-initializer-list­

>variable-declaration → variable-declaration-head ­variable-name ­type-annotation ­code-block­

>variable-declaration → variable-declaration-head ­variable-name ­type-annotation ­getter-setter-block­

>variable-declaration → variable-declaration-head ­variable-name­ type-annotation ­getter-setter-keyword-block­

 > variable-declaration → variable-declaration-head­ variable-name ­type-annotation­initializer­ opt ­willSet-didSet-block­

>variable-declaration-head → attributes ­opt­ declaration-specifiers ­opt ­var
­
>variable-name → identifier­

>getter-setter-block → {­getter-clause ­setter-clause­ opt­}­

>getter-setter-block → {­setter-clause ­getter-clause­}­

>getter-clause → attributes ­opt­get­code-block­

>setter-clause → attributes ­opt ­set­ setter-name­ opt­ code-block­

>setter-name → (­identifier­)­

>getter-setter-keyword-block → {­getter-keyword-clause ­setter-keyword-clause­ opt­}
­
>getter-setter-keyword-block → {­setter-keyword-clause ­getter-keyword-clause­}

>getter-keyword-clause → attributes­ opt­ get­

>setter-keyword-clause → attributes ­opt­ set­

>willSet-didSet-block → {­willSet-clause ­didSet-clause ­opt­}­

>willSet-didSet-block → {­didSet-clause ­willSet-clause­}­

>willSet-clause → attributes ­opt ­willSet ­setter-name­ opt ­code-block­

>didSet-clause → attributes ­opt ­didSet ­setter-name ­opt­ code-bloc


##Type Alias Declaration

##类型的别名声明

A type alias declaration introduces a named alias of an existing type into your program. Type alias declarations begin with the keyword typealias and have the following form:

类型alias声明引入了一个存在类型的名字到你的程序当中。类型alias声明以关键字typelias开头，使用一下的形式：

  typealias name = existing type
  
After a type alias is declared, the aliased name can be used instead of the existing type everywhere in your program. The existing type can be a named type or a compound type. Type aliases do not create new types; they simply allow a name to refer to an existing type.

在一个类型alias声明后，声明的名字可以使用在你的程序的的任何地方使用了。存在的类型可能是一个命令类型或是计算类型。类型 alias不能创造新类型，他们只是简单的把名字指向一个存在的类型。

See also Protocol Associated Type Declaration.

也可以参看Protocol Associated Type Declaration.

>GRAMMAR OF A TYPE ALIAS DECLARATION


> typealias-declaration → typealias-head­ typealias-assignment
> typealias-head → typealias­ typealias-name
> typealias-name → identifier
> typealias-assignment → =type

##Function Declaration

##函数声明

A :newTerm`function declaration` introduces a function or method into your program. A function declared in the context of class, structure, enumeration, or protocol is referred to as a method. Function declarations are declared using the keyword func and have the following form:

一个新术语”函数声明“引入了一个函数或者方法到程序中。在类，结构，枚举或者协议韩经理声明的函数会被挡住函数。番薯声明使用关键字func声明，采用以下的形式。

  func function name(parameters) -> return type {
    statements
  }
If the function has a return type of Void, the return type can be omitted as follows:

如果函数有void的返回类型，返回类型可像下面这样忽略：

func function name(parameters) {
    statements
}
The type of each parameter must be included—it can’t be inferred. By default, the parameters to a function are constants. Write var in front of a parameter’s name to make it a variable, scoping any changes made to the variable just to the function body, or write inout to make those changes also apply to the argument that was passed in the caller’s scope. For a discussion of in-out parameters, see In-Out Parameters.

每个参数的类型必须包含-不能通过推断。默认情况下，函数的参数是常量。在参数名的前面写一个var会让他成为一个变量，对变量的做的任何变化只会在函数体力有效，或者写入input使这些改变也会应用唉调用者范围的参数。

Functions can return multiple values using a tuple type as the return type of the function.

函数可以使用元组类型作为函数的返回类型来返回多个值

A function definition can appear inside another function declaration. This kind of function is known as a nested function. For a discussion of nested functions, see Nested Functions.

函数定义可以出现在另一个函数声明之内。这种函数叫做嵌入函数。对于嵌入函数的讨论，请参见Nested Function。

Parameter Names

Function parameters are a comma separated list where each parameter has one of several forms. The order of arguments in a function call must match the order of parameters in the function’s declaration. The simplest entry in a parameter list has the following form:

函数参数是一个逗号分隔的列表，每个参数可以有好几种形式。函数调用的时候参数的顺序必须匹配函数声明的参数顺序。在参数列表里最简单的输入形式：

  parameter name: parameter type


For function parameters, the parameter name is used within the function body, but is not used when calling the function. For method parameters, the parameter name is used as within the function body, and is also used as a label for the argument when calling the method. The name of a method’s first parameter is used only within the function body, like the parameter of a function. For example:

对于函数参数，参数名字在函数体内部使用，但是在调用函数的时候不会使用。对于方法参数，参数名可以在函数体使用，也在调用方法时可以作为参数的标签使用。函数的一个参数名字仅仅在函数体力使用，就像函数的参数。例如


func f(x: Int, y: String) -> String {
        return y + String(x)
    }
    f(7, "hello")  // x and y have no name

    class C {
        func f(x: Int, y: String) -> String {
           return y + String(x)
        }
    }
    let c = C()
    c.f(7, y: "hello")  // x没有名称，y有名称


You can override the default behavior for how parameter names are used with one of the following forms:

你可以重写参数名字使用的默认行为，采用如下的形式：


  external parameter name local parameter name: parameter type
    #parameter name: parameter type
    _ local parameter name: parameter type


A second name before the local parameter name gives the parameter an external name, which can be different than the local parameter name. The external parameter name must be used when the function is called. The corresponding argument must have the external name in function or method calls.

本地参数名的在第二个名字给参数了一个外部的名字，这个不同于本地的参数名。外部的参数名必须在函数调用的时候调用。相应的参数必须在函数或者方法调用时有外部名字。

A hash symbol (#) before a parameter name indicates that the name should be used as both an external and a local parameter name. It has the same meaning as writing the local parameter name twice. The corresponding argument must have this name in function or method calls.

参数名前的#显示了名字应该被作为外部和本地参数只哟个。它和写入本地参数名两次有同样的意义。嘴硬的参数在函数或者参数调用时必须有这个名字。

An underscore (_) before a local parameter name gives that parameter no name to be used in function calls. The corresponding argument must have no name in function or method calls.

本次参数名的下划线在函数调用的时候让参数没有使用名字。对应的参在函数或者方法调用的时候不可以有名字。

##Special Kinds of Parameters

##特殊类型的参数

Parameters can be ignored, take a variable number of values, and provide default values using the following forms:
参数可以忽略，可以是可变数量的值，使用如下的形式提供默认值


 _ : <#parameter type#.
    parameter name: parameter type...
    parameter name: parameter type = default argument value


A parameter named with an underscore (_) is explicitly ignored an can’t be accessed within the body of the function.

带有下划线的参数会显式的被忽略，在函数体内部不能被访问到。

A parameter with a base type name followed immediately by three dots (...) is understood as a variadic parameter. A function can have at most one variadic parameter, which must be its last parameter. A variadic parameter is treated as an array that contains elements of the base type name. For instance, the variadic parameter Int... is treated as Int[]. For an example that uses a variadic parameter, see Variadic Parameters.

带有基本类型后面接着3个点的参数。

A parameter with an equals sign (=) and an expression after its type is understood to have a default value of the given expression. If the parameter is omitted when calling the function, the default value is used instead. If the parameter is not omitted, it must have its name in the function call. For example, f() and f(x: 7) are both valid calls to a function with a single default parameter named x, but f(7) is invalid because it provides a value without a name.

带有等号（=）的参数和它类型后面的表达式会被仿作给定表达式的默认类型。如果参数在调用函数的时候被忽略，默认值会被使用。例如，f()和f(x:7)都是有效的调用对于带有单个默认的的参数名x的函数，但是f(7)是有效的，因为它提供了没有名字的值。

Special Kinds of MethodsMethods on an enumeration or a structure that modify self must be marked with the mutating keyword at the start of the function declaration.

枚举类型或者结构上的方法，会修改self的必须在函数声明的开始标记为mutating关键字

Methods that override a superclass method must be marked with the override keyword at the start of the function declaration. It is an error to override a method without the override keyword or to use the overridekeyword on a method that doesn’t override a superclass method.

重写超类方法的方法必须在函数声明的开头override关键词标记。不适用override就重写方法会产生错误或者使用override在没有override超类的方法

Methods associated with a type rather than an instance of a type must be marked with the static attribute for enumerations and structures or the class attribute for classes.

与type相关而不是类型实例相关的方法必须使用使用static属性来标记枚举、结构或者类的class属性

##Curried Functions and Methods

##科里化函数和方法

Curried functions and methods have the following form:

科里化函数和方法有以下的形式：


  func function name(parameters)(parameters) -> return type {
        statements
    }

以这种形式定义的函数的返回值是另一个函数。举例来说，下面的两个声明时等价的:

 func addTwoNumbers(a: Int)(b: Int) -> Int {
        return a + b
    }
    func addTwoNumbers(a: Int) -> (Int -> Int) {
        func addTheSecondNumber(b: Int) -> Int {
            return a + b
        }
        return addTheSecondNumber
    }

    addTwoNumbers(4)(5) // Returns 9

多级柯里化应用如下

>GRAMMAR OF A FUNCTION DECLARATION

>function-declaration → function-head­ function-name­ generic-parameter-clause ­opt­function-signature­ function-body­
> function-head → attributes ­opt ­declaration-specifiers ­opt ­func­
> function-name → identifier­  operator­
>function-signature → parameter-clauses ­function-result ­opt­
> function-result → ->­attributes ­opt ­type­
>  function-body → code-block­
>  parameter-clauses → parameter-clause ­parameter-clauses ­opt­
>  parameter-clause → (­)­  (­parameter-list­...­opt­)­
>  parameter-list → parameter­  parameter­,­parameter-list­
> parameter → inout ­opt ­let ­opt­#­opt­parameter-name local-parameter-name ­opt­ type-annotation ­default-argument-clause ­opt­
> parameter → inout­opt­var­#­opt­parameter-name­local-parameter-name ­opt­ type-annotation­default-argument-clause ­opt­
> parameter → attributes ­opt ­type­
> parameter-name → identifier­  _­
>  local-parameter-name → identifier­  _­
>  default-argument-clause → =­expression­：

A function declared this way is understood as a function whose return type is another function. For example, the following two declarations are equivalent:

用这种方式声明的函数会被当做一个函数，这个函数的返回类型是另外一个函数。例如，下面2个声明是一样的：


##Enumeration Declaration

##枚举声明

An enumeration declaration introduces a named enumeration type into your program.

枚举声明引入一个个名叫枚举的类型到你的程序中。


Enumeration declarations have two basic forms and are declared using the keyword enum. The body of an enumeration declared using either form contains zero or more values—called enumeration cases—and any number of declarations, including computed properties, instance methods, static methods, initializers, type aliases, and even other enumeration, structure, and class declarations. Enumeration declarations can’t contain destructor or protocol declarations.

枚举声明有2中基本的形式，使用关键字enum声明。一个枚举类型的的主题使用2中形式之一，包含0或者蒙多的值-被称作枚举类型还有任何数量的声明，包括可计算的属性，实例方法，静态方法，初始化，类型aliase,和其它的枚举、结构和类声明。枚举声明不能包含析构或者协议声明。

Unlike classes and structures, enumeration types do not have an implicitly provided default initializer; all initializers must be declared explicitly. Initializers can delegate to other initializers in the enumeration, but the initialization process is complete only after an initializer assigns one of the enumeration cases to self.

不像类或者结构，枚举类型没有一个默认的初始化，但是初始化过程仅仅在初始化赋值给枚举类型的一个给self的时候。

Like structures but unlike classes, enumerations are value types; instances of an enumeration are copied when assigned to variables or constants, or when passed as arguments to a function call. For information about value types, see Structures and Enumerations Are Value Types.

类似结构但是不像类，枚举累心是值类型；一个枚举实例在赋值给变量或者常量的时候会被复制，或者在传递参数给函数调用的的时候。

You can extend the behavior of an enumeration type with an extension declaration, as discussed inExtension Declaration.

Enumerations with Cases of Any Type

The following form declares an enumeration type that contains enumeration cases of any type:

下面的形式声明了一个枚举类型，包含了所有类型的枚举。


   enum enumeration name {
        case enumeration case 1
        case enumeration case 2(associated value types)
    }



Enumerations declared in this form are sometimes called discriminated unions in other programming languages.

用这种形式声明的枚举在其他语言里有时候被叫做discriminated unions

In this form, each case block consists of the keyword case followed by one or more enumeration cases, separated by commas. The name of each case must be unique. Each case can also specify that it stores values of a given type. These types are specified in the associated value types tuple, immediately following the name of the case. For more information and to see examples of cases with associated value types, seeAssociated Values.

用这种方式，每个cast块由关键字case组成，case后跟着一个或者多个逗号分隔的枚举情况。每个case的名字必须是唯一的。每个case页能够确定他存储一个给定类型的值。这些类型用关联只类型元组来设置，后面紧梗着case的名字。获取更多信息，看下关联至类型的的例子，请看Assiciated Values Enumerations with Raw Cases Values

The following form declares an enumeration type that contains enumeration cases of the same basic type:

下面的形式声明了一种枚举类型，包含同样基本类型的枚举case


    enum enumeration name: raw value type {
        case enumeration case 1 = raw value 1
        case enumeration case 2 = raw value 2
    }



In this form, each case block consists of the keyword case, followed by one or more enumeration cases, separated by commas. Unlike the cases in the first form, each case has an underlying value, called a raw value, of the same basic type. The type of these values is specified in the raw value type and must represent a literal integer, floating-point number, character, or string.

通过这种形式，每种caes块是由关键字case后面跟着一个或者多个由多个逗号分隔的枚举case。不像第一种形式的case，每个case有一个underlying值，叫做原生值。这些值的类型在rsw值的类型设置，必须表示一个字面量整数，浮点数，字符和字符串。

Each case must have a unique name and be assigned a unique raw value. If the raw value type is specified as Int and you don’t assign a value to the cases explicitly, they are implicitly assigned the values 0, 1, 2, and so on. Each unassigned case of type Int is implicitly assigned a raw value that is automatically incremented from the raw value of the previous case.

每个case必须有一个唯一的名字，然后被赋值为一个单独的原生值。如果原生值用Int设置，你不需要要显式的赋值，他们可以默认的赋值1,1,2等等。每个没有赋值的Int类型会被赋值为原生类型，可以自动的从之前的case的原生值增加。


	enum ExampleEnum: Int {
	    case A, B, C = 5, D
	}


In the above example, the value of ExampleEnum.A is 0 and the value of ExampleEnum.B is 1. And because the value of ExampleEnum.C is explicitly set to 5, the value of ExampleEnum.D is automatically incremented from 5 and is therefore 6.

在上面的例子中，ExampleEnum。A的值是o.ExampleEnum.B值是1。因为ExampleEnum.C是显式的设置为5，ExampleEnumd.D的值会从5自动的增加，所以是6.

The raw value of an enumeration case can be accessed by calling its toRaw method, as inExampleEnum.B.toRaw(). You can also use a raw value to find a corresponding case, if there is one, by calling the fromRaw method, which returns an optional case. For more information and to see examples of cases with raw value types, see Raw Values.

枚举类型的原生值可以通过toRaw方法访问，比如ExampleEnum.B.toRaw()。你也可以使用一个原生值来找到对应的case通过调用fromRaw方法。

##Accessing Enumeration Cases

##访问枚举case

To reference the case of an enumeration type, use dot (.) syntax, as in EnumerationType.EnumerationCase. When the enumeration type can be inferred from context, you can omit it (the dot is still required), as described inEnumeration Syntax and Implicit Member Expression.

正如EnumerationType.EnumerationCase，可以使用。来引用一个enumeration类型的case，正如inEnumeration Syntax and Implicit Member Expression.描述的。

To check the values of enumeration cases, use a switch statement, as shown in Matching Enumeration Values with a Switch Statement. The enumeration type is pattern-matched against the enumeration case patterns in the case blocks of the switch statement, as described in Enumeration Case Pattern.

>GRAMMAR OF AN ENUMERATION DECLARATION

>   enum-declaration → attributes­opt­union-style-enum­  attributes­opt­raw-value-style-enum­
>    union-style-enum → enum-name­generic-parameter-clause­opt­{­union-style-enum-members­opt­}­
    union-style-enum-members → union-style-enum-member­union-style-enum-members­opt­
    union-style-enum-member → declaration­  union-style-enum-case-clause­
    union-style-enum-case-clause → attributes­opt­case­union-style-enum-case-list­
    union-style-enum-case-list → union-style-enum-case­  union-style-enum-case­,­union-style-enum-case-list­
    union-style-enum-case → enum-case-name­tuple-type­opt­
    enum-name → identifier­
    enum-case-name → identifier­
    raw-value-style-enum → enum-name­generic-parameter-clause­opt­:­type-identifier­{­raw-value-style-enum-members­opt­}­
    raw-value-style-enum-members → raw-value-style-enum-member­raw-value-style-enum-members­opt­
    raw-value-style-enum-member → declaration­  raw-value-style-enum-case-clause­
    raw-value-style-enum-case-clause → attributes­opt­case­raw-value-style-enum-case-list­
    raw-value-style-enum-case-list → raw-value-style-enum-case­  raw-value-style-enum-case­,­raw-value-style-enum-case-list­
    raw-value-style-enum-case → enum-case-name­raw-value-assignment­opt­
    raw-value-assignment → =­literal­

Structure Declaration

A structure declaration introduces a named structure type into your program. Structure declarations are declared using the keyword struct and have the following form:

一个结构声明引入了一个命名的类型到你的程序。结构声明使用struct声明，采用以下的形式：

   struct structure name: adopted protocols {
     declarations
   }


The body of a structure contains zero or more declarations. These declarations can include both stored and computed properties, static properties, instance methods, static methods, initializers, type aliases, and even other structure, class, and enumeration declarations. Structure declarations can’t contain destructor or protocol declarations. For a discussion and several examples of structures that include various kinds of declarations, see Classes and Structures.

结构体包含0或者更多的声明。这个声明能包括可存储和计算的属性，静态属性，示例方法，静态方法，实例化，type aliases，甚至其他结构，类和枚举声明。结构声明不能包含析构或者协议声明。在Classes and Structures里，包括好几种了类型的声明的桃花好几个结构例子。

Structure types can adopt any number of protocols, but can’t inherit from classes, enumerations, or other structures.

结构类型可以采用任何数量的协议，但是从classes继承，枚举或者其他结构。

There are three ways create an instance of a previously declared structure:

有3种方式创建过去声明过的示例结构的示例。


	* Call one of the initializers declared within the structure, as described in Initializers.
          就像Initializers描述的，调用结构里的一个初始器之一。

	* If no initializers are declared, call the structure’s memberwise initializer, as described in Memberwise Initializers for Structure Types.
         如果没有初始器被声明，就可以调用结构区的成员

	* If no initializers are declared, and all properties of the structure declaration were given initial values, call the structure’s default initializer, as described in Default Initializers.
          如果没有初始化器被声明，结构所有其他声明的属性就会被给予初始化的值，调用结构的某人初始化器，正如Default Initializers    .描述的那样。 



The process of initializing a structure’s declared properties is described in Initialization.

初始化结构的声明的属性的过程在Initialization里描述的一样。

Properties of a structure instance can be accessed using dot (.) syntax, as described in Accessing Properties.

一个结构实例的属性使用通过。语法来访问。

Structures are value types; instances of a structure are copied when assigned to variables or constants, or when passed as arguments to a function call. For information about value types, see Structures and Enumerations Are Value Types.

结构是值类型；一个结构的实例复制在赋值给变量或者常量或者在传递参数给函数调用的时候。关于值类型的信息，请参看Structures and Enumerations Are Value Types.

You can extend the behavior of a structure type with an extension declaration, as discussed in Extension Declaration.
你可以用一个扩展声明来扩展一个结构类型的行为，正如Extension Declaration讨论的。

>GRAMMAR OF A STRUCTURE DECLARATION

>    struct-declaration → attributes­opt­struct­struct-name­generic-parameter-clause­opt­type-inheritance-clause­opt­struct-body­
>    struct-name → identifier­
>    struct-body → {­declarations­opt­}

##Class Declaration

##类声明


A class declaration introduces a named class type into your program. Class declarations are declared using the keyword class and have the following form:

类型声明映入了一个命令的类型到你的程序中。类声明使用关键字class声明，采用下面的形式：


    class class name: superclass, adopted protocols {
        declarations
    }


The body of a class contains zero or more declarations. These declarations can include both stored and computed properties, instance methods, class methods, initializers, a single destructor method, type aliases, and even other class, structure, and enumeration declarations. Class declarations can’t contain protocol declarations. For a discussion and several examples of classes that include various kinds of declarations, see Classes and Structures.

一个class的主题会包含0或多个声明。这些声明可以包括可存储的和可计算的属性，实例方法，类方法，初始化器，一个析构函数，type aliases ，和甚至其他的class，结构，枚举声明。类声明不能包括是协议声明。

A class type can inherit from only one parent class, its superclass, but can adopt any number of protocols. The superclass appears first in the type-inheritance-clause, followed by any adopted protocols.
一个class类只能从一个父类中继承，但是可以有多个洗衣。超类首先出现在类型继承语句中，后面跟着采用的协议。

As discussed in Initializer Declaration, classes can have designated and convenience initializers. When you declare either kind of initializer, you can require any subclass to override it by marking the initializer with therequired attribute. The designated initializer of a class must initialize all of the class’s declared properties and it must do so before calling any of its superclass’s designated initializers.

正如在初始化声明讨论的一样，类的初始化很特别很便利。当你声明不同种类的初始化器时，你可以使用required属性要求任何子类重写他。这个特定的初始化器必须初始化类的所有声明的属性。在调用任何自雷的特定的初始化器时都必须这么做。

A class can override properties, methods, and initializers of its superclass. Overridden methods and properties must be marked with the override keyword.

类可以重写他的超类的属性，方法和初始化器。重写的方法和属性必须都使用overrid来标记。

Although properties and methods declared in the superclass are inherited by the current class, designated initializers declared in the superclass are not. That said, if the current class overrides all of the superclass’s designated initializers, it inherits the superclass’s convenience initializers. Swift classes do not inherit from a universal base class.

尽管在子类中声明的属性和方法可以被当前的类继承，但是在超类中指定的初始化器却不行。也就是说，如果当前类重写了超类的所有指定的初始化器，它就会继续超类的便利的初始化器。Swift类不会从通用的基类中继承。

There are two ways create an instance of a previously declared class:

有两种方式创建过去声明的类的实例：


	* Call one of the initializers declared within the class, as described in Initializers.
         在类的内部调用声明的初始化器。

	* If no initializers are declared, and all properties of the class declaration were given initial values, call the class’s default initializer, as described in Default Initializers.

       如果没有声明的初始化器，类声明的素有属性会有一个初始化值，是通过调用类的默认的初始化器来完成的。正如Default Initializers描述的。



Access properties of a class instance with dot (.) syntax, as described in Accessing Properties.

访问类的属性使用，如Accessing Properties的一样。


Classes are reference types; instances of a class are referred to, rather than copied, when assigned to variables or constants, or when passed as arguments to a function call. For information about reference types, see Structures and Enumerations Are Value Types.

类是引用类型；在被赋值给变量货常量的时候，类的实例会被引用而不是被赋值，当被作为参数传递给函数调用的时候。更多信息，参考
 Structures and Enumerations Are Value Types.。


You can extend the behavior of a class type with an extension declaration, as discussed in Extension Declaration.

你可以使用extension声明来扩展类的行为，正如Extension Desclaration.


 >  GRAMMAR OF A CLASS DECLARATION
 >   class-declaration → attributes­opt­class­class-name­generic-parameter-clause­opt­type-inheritance-clause­opt­class-body­
 >   class-name → identifier­
 >  class-body → {­declarations­opt­}

##Protocol Declaration

##协议声明

A protocol declaration introduces a named protocol type into your program. Protocol declarations are declared using the keyword protocol and have the following form:

一个协议声明引入了一命令协议类型到你的程序中。协议声明可以使用protoco来声明，有如下的形式：


  protocol protocol name: inherited protocols {
     protocol member declarations
  }

The body of a protocol contains zero or more protocol member declarations, which describe the conformance requirements that any type adopting the protocol must fulfill. In particular, a protocol can declare that conforming types must implement certain properties, methods, initializers, and subscripts. Protocols can also declare special kinds of type aliases, called associated types, that can specify relationships among the various declarations of the protocol. The protocol member declarations are discussed in detail below.

协议的主体包含洗衣成员声明，它描述了comformance要求，任何实现它的协议都必须满足的要求。特别是，协议可以声明comformin类型，必须实现某个属性，方法，初始化，和子脚本。协议页能声明特殊种类的typealiase,被称作关联类型，可以设置协议里的不同声明的关系。协议成员声明下面会做详细的讨论。

Protocol types can inherit from any number of other protocols. When a protocol type inherits from other protocols, the set of requirements from those other protocols are aggregated, and any type that inherits from the current protocol must conform to all those requirements. For an example of how to use protocol inheritance, see Protocol Inheritance.

协议类型可以从任何数量的其它协议。当一个协议类型从其它洗衣继承时，从那些协议中的要求会被集合，任何从当前协议继承的类型都必须和那些要求一致。


NOTE
You can also aggregate the conformance requirements of multiple protocols using protocol composition types, as described in Protocol Composition Type and Protocol Composition.

You can add protocol conformance to a previously declared type by adopting the protocol in an extension declaration of that type. In the extension, you must implement all of the adopted protocol’s requirements. If the type already implements all of the requirements, you can leave the body of the extension declaration empty.

你可以增加协议conformance到任何一个过去声明的类型通过在那个类型的extendsion中声明。在这个扩展力，你必须实现所有使用的协议的需求。如果那个类型已经实现了所有的要求，扩展声明的主题可以是空的。

By default, types that conform to a protocol must implement all properties, methods, and subscripts declared in the protocol. That said, you can mark these protocol member declarations with the optional attribute to specify that their implementation by a conforming type is optional. The optional attribute can be applied only to protocols that are marked with the objc attribute. As a result, only class types can adopt and conform to a protocol that contains optional member requirements. For more information about how to use the optionalattribute and for guidance about how to access optional protocol members—for example, when you’re not sure whether a conforming type implements them—see Optional Protocol Requirements.

默认情况下，与协议一致的类型必须实现所有的属性，方法，和声明的subscripts。也就是说，你可以用opaional属性来标记协议成员，表示他们的实现是可选的。option属性仅仅能被应用到用objc标记的属性。结构，仅仅class类型能采纳和玉包含可选的成员变量的协议一致。对于如何访问可选的协议成员-例如，如果你不确定一个confroming类型是否要实现他们-看见 Optional Protocol Requirements.

To restrict the adoption of a protocol to class types only, mark the entire protocol declaration with theclass_protocol attribute. Any protocol that inherits from a protocol marked with the class_protocol attribute can likewise be adopted only by a class type.

为了限制协议的的只应用到某个class type，用class_protocol属性标记整个协议声明。任何从标记class_protocol协议继承的协议可以只被class 类型采纳。

NOTE
If a protocol is already marked with the objc attribute, the class_protocol attribute is implicitly applied to that protocol; there’s no need to mark the protocol with the class_protocol attribute explicitly.

Protocols are named types, and thus they can appear in all the same places in your code as other named types, as discussed in Protocols as Types. However, you can’t construct an instance of a protocol, because protocols do not actually provide the implementations for the requirements they specify.


You can use protocols to declare which methods a delegate of a class or structure should implement, as described in Delegation.
你可以使用协议来声明类或者结构应该实现那个方法，如Delegation.描述。


>协议声明的语法
protocol-declaration → attributes­opt­protocol­protocol-name­type-inheritance-clause­opt­protocol-body­
protocol-name → identifier­
protocol-body → {­protocol-member-declarations­opt­}­
protocol-member-declaration → protocol-property-declaration­
protocol-member-declaration → protocol-method-declaration­
protocol-member-declaration → protocol-initializer-declaration­
protocol-member-declaration → protocol-subscript-declaration­
protocol-member-declaration → protocol-associated-type-declaration­
protocol-member-declarations → protocol-member-declaration­protocol-member-declarations­opt­

##Protocol Property Declaration

##协议属性声明

Protocols declare that conforming types must implement a property by including a protocol property declaration in the body of the protocol declaration. Protocol property declarations have a special form of a variable declaration:

var property name: type { get set }
As with other protocol member declarations, these property declarations declare only the getter and setter requirements for types that conform to the protocol. As a result, you don’t implement the getter or setter directly in the protocol in which it is declared.

The getter and setter requirements can be satisfied by a conforming type in a variety of ways. If a property declaration includes both the get and set keywords, a conforming type can implement it with a stored variable property or a computed property that is both readable and writeable (that is, one that implements both a getter and a setter). However, that property declaration can’t be implemented as a constant property or a read-only computed property. If a property declaration includes only the get keyword, it can be implemented as any kind of property. For examples of conforming types that implement the property requirements of a protocol, see Property Requirements.

See also Variable Declaration.

GRAMMAR OF A PROTOCOL PROPERTY DECLARATION

protocol-property-declaration → variable-declaration-head­variable-name­type-annotation­getter-setter-keyword-block­


##Protocol Method Declaration

##协议方法声明

Protocols declare that conforming types must implement a method by including a protocol method declaration in the body of the protocol declaration. Protocol method declarations have the same form as function declarations, with two exceptions: They don’t include a function body, and you can’t provide any default parameter values as part of the function declaration. For examples of conforming types that implement the method requirements of a protocol, see Method Requirements.

协议表明，conforming类型必须在协议声明体里通过包括一个协议方法声明来实现方法。协议方法声明与函数声明有同样的形式，只有2点例外：他们不需要包括函数体，你不能提供任何某人参数值作为函数声明的一部分。


To declare a class or static method requirement in a protocol declaration, mark the method declaration with the class keyword. Classes that implement this method also declare the method with the class keyword. Structures that implement it must declare the method with the static keyword instead. If you’re implementing the method in an extension, use the class keyword if you’re extending a class and the static keyword if you’re extending a structure.

在协议声明里，为了声明一个类或者静态方法要求，使用class关键字来标记方法声明。实现这个方法的类也用class来声明方法。实现它的结构必须用static进行声明。如果你在extension里实现，如果你扩展class使用class，如果是结构使用static


>GRAMMAR OF A PROTOCOL METHOD DECLARATION

>protocol-method-declaration → function-head­function-name­generic-parameter-clause­opt­function-signature­

##Protocol Initializer Declaration
##协议构造器声明

Protocols declare that conforming types must implement an initializer by including a protocol initializer declaration in the body of the protocol declaration. Protocol initializer declarations have the same form as initializer declarations, except they don’t include the initializer’s body.

See also Initializer Declaration.

>GRAMMAR OF A PROTOCOL INITIALIZER DECLARATION

>protocol-initializer-declaration → initializer-head­generic-parameter-clause­opt­parameter-clause­


##Protocol Subscript Declaration

Protocols declare that conforming types must implement a subscript by including a protocol subscript declaration in the body of the protocol declaration. Protocol property declarations have a special form of a subscript declaration:


>subscript (parameters) -> return type { get set }


Subscript declarations only declare the minimum getter and setter implementation requirements for types that conform to the protocol. If the subscript declaration includes both the get and set keywords, a conforming type must implement both a getter and a setter clause. If the subscript declaration includes only the get keyword, a conforming type must implement at least a getter clause and optionally can implement a setter clause.
See also Subscript Declaration.

>GRAMMAR OF A PROTOCOL SUBSCRIPT DECLARATION

>protocol-subscript-declaration → subscript-head­subscript-result­getter-setter-keyword-block­

##Protocol Associated Type Declaration

##协议关联类型声明

Protocols declare associated types using the keyword typealias. An associated type provides an alias for a type that is used as part of a protocol’s declaration. Accosiated types are similiar to type paramters in generic parameter clauses, but they’re associated with Self in the protocol in which they’re declared. In that context, Self refers to the eventual type that conforms to the protocol. For more information and examples, see Associated Types.

协议用关键字typealias声明关联类型。关联类型为类型提供了一个alias，这个被用作协议声明的一部分。关联类型与在通用参数预计的类型参数相似，但是他们与声明他们的协议中的self相似。在那个环境下，self指的是时间类型。

See also Type Alias Declaration.

>GRAMMAR OF A PROTOCOL ASSOCIATED TYPE DECLARATION

>protocol-associated-type-declaration → typealias-head­type-inheritance-clause­opt­typealias-assignment­op

An initializer declaration introduces an initializer for a class, structure, or enumeration into your program. Initializer declarations are declared using the keyword init and have two basic forms.

实例化声明引入了类的初始化器到程序里。初始化声明使用关键字init声明，有两种基本形式：

Structure, enumeration, and class types can have any number of initializers, but the rules and associated behavior for class initializers are different. Unlike structures and enumerations, classes have two kinds of initializers: designated initializers and convenience initializers, as described in Initialization.

结构，枚举和类类型可以有很多初始器，但是class初始化器的规则和关联行为是不同的。不像结构和枚举类型。类有两种初始化器：制定的和便利的初始化器。
The following form declares initializers for structures, enumerations, and designated initializers of classes:


    init(parameters) {
         statements
    }


A designated initializer of a class initializes all of the class’s properties directly. It can’t call any other initializers of the same class, and if the class has a superclass, it must call one of the superclass’s designated initializers. If the class inherits any properties from its superclass, one of the superclass’s designated initializers must be called before any of these properties can be set or modified in the current class.
Designated initializers can be declared in the context of a class declaration only and therefore can’t be added to a class using an extension declaration.
Initializers in structures and enumerations can call other declared initializers to delegate part or all of the initialization process.
To declare convenience initializers for a class, prefix the initializer declaration with the context-sensitive keyword convenience.


    convenience init(parameters) {
       statements
    }


Convenience initializers can delegate the initialization process to another convenience initializer or to one of the class’s designated initializers. That said, the initialization processes must end with a call to a designated initializer that ultimately initializes the class’s properties. Convenience initializers can’t call a superclass’s initializers.
You can mark designated and convenience initializers with the required attribute to require that every subclass implement the initializer. Because designated initializers are not inherited by subclasses, they must be implemented directly. Required convenience initializers can be either implemented explicitly or inherited when the subclass directly implements all of the superclass’s designated initializers (or overrides the designated initializers with convenience initializers). Unlike methods, properties, and subscripts, you don’t need to mark overridden initializers with the override keyword.

To see examples of initializers in various type declarations, see Initialization.


>GRAMMAR OF AN INITIALIZER DECLARATION

>initializer-declaration → initializer-head­generic-parameter-clause­opt­parameter-clause­initializer-body­
>initializer-head → attributes­opt­convenience­opt­init­
>initializer-body → code-block­

A deinitializer declaration declares a deinitializer for a class type. Deinitializers take no parameters and have the following form:

析构声明在类中声明了一个析构器。析构器不需要参数，遵循如下的格式：

    deinit {
       statements
    }


A deinitializer is called automatically when there are no longer any references to a class object, just before the class object is deallocated. A deinitializer can be declared only in the body of a class declaration—but not in an extension of a class—and each class can have at most one.

当类中没有对任何其它对象的引用时，在类对象释放之前，析构器会自动的被调用。析构器只能在类的声明体内、声明——但是不能在 类的扩展声明内，每个类最多只能有一个析构器声明。

A subclass inherits its superclass’s deinitializer, which is implicitly called just before the subclass object is deallocated. The subclass object is not deallocated until all deinitializers in its inheritance chain have finished executing.


Deinitializers are not called directly.

子类继承了它的超类的析构器，在子类帝乡将要被释放时会被隐式的调用。子类在所有析构器被执行完毕前不会被释放。
析构器不会被直接调用。

For an example of how to use a deinitializer in a class declaration, see Deinitialization.
>GRAMMAR OF A DEINITIALIZER DECLARATION

>deinitializer-declaration → attributes­opt­deinit­code-block

##Extension Declaration
##扩展声明

An extension declaration allows you to extend the behavior of existing class, structure, and enumeration types. Extension declarations begin with the keyword extension and have the following form:

扩展声明用于扩展一个已存在的类，结构体，枚举的行为。扩展声明以关键字extension开始，有如下的形式：



    extension type: adopted protocols {
       declarations
    }



The body of an extension declaration contains zero or more declarations. These declarations can include computed properties, computed static properties, instance methods, static and class methods, initializers, subscript declarations, and even class, structure, and enumeration declarations. Extension declarations can’t contain destructor or protocol declarations, store properties, property observers, or other extension declarations. For a discussion and several examples of extensions that include various kinds of declarations, see Extensions.

扩展声明体包括零个或多个声明。这些声明可以包括计算型属性，计算型静态属性，实例方法，静态和类方法，构造器，附属脚本声明，甚至其它类，结构和枚举声明。扩展声明不能包含析构器，协议声明，存储型属性，属性监测器或其它的扩展属性。详细讨论和查看包含多种扩展声明的实例，参见Extensions一节。

Extension declarations can add protocol conformance to an existing class, structure, and enumeration type in the adopted protocols. Extension declarations can’t add class inheritance to an existing class, and therefore the type-inheritance-clause in an extension declaration contains only a list of protocols.

扩展声明可以向存在的类，结构体，枚举添加一致的协议。扩展声明不能向一个类中添加类的继承，因此type-inheritance-clause只包含协议的列表。


Properties, methods, and initializers of an existing type can’t be overridden in an extension of that type.
现存类型的属性，方法，构造器不能被它们的扩展重写。

Extension declarations can contain initializer declarations. That said, if the type you’re extending is defined in another module, an initializer declaration must delegate to an initializer already defined in that module to ensure members of that type are properly initialized.
扩展声明可以包含构造器声明，这意味着，如果你扩展的类型在其他模块中定义，构造器声明必须委托另一个在 那个模块里声明的构造器来恰当的初始化。

>GRAMMAR OF AN EXTENSION DECLARATION

>extension-declaration → extension­type-identifier­type-inheritance-clause­opt­extension-body­
>extension-body → {­declarations­opt­}­


##Subscript Declaration

##附属脚本声明

A subscript declaration allows you to add subscripting support for objects of a particular type and are typically used to provide a convenient syntax for accessing the elements in a collection, list, or sequence. Subscript declarations are declared using the keyword subscript and have the following form:

附属脚本声明用于向特定类型的对象添加附属脚本支持，通常为访问集合，列表和序列的元素提供便利的语法。使用关键字subscript，声明形式如下：


> subscript (`parameter`) -> (return type){
    get{
      `statements`
    }
    set(`setter name`){
      `statements`
    }
}


Subscript declarations can appear only in the context of a class, structure, enumeration, extension, or protocol declaration.

附属脚本声明只能出现在类，结构，枚举类型，扩展或协议声明的上下文中。

The parameters specify one or more indexes used to access elements of the corresponding type in a subscript expression (for example, the i in the expression object[i]). Although the indexes used to access the elements can be of any type, each parameter must include a type annotation to specify the type of each index. The return type specifies the type of the element being accessed.

参数(parameters)指定了一个或多个用于在相应类型的附属脚本表达式中访问元素的索引（例如，表达式object[i]中的i）。尽管用于访问元素的索引可以是任意类型，但是每个参数必须包含一个类型标注来指定每种索引的类型。返回类型(return type)指定被访问的元素的类型。


As with computed properties, subscript declarations support reading and writing the value of the accessed elements. The getter is used to read the value, and the setter is used to write the value. The setter clause is optional, and when only a getter is needed, you can omit both clauses and simply return the requested value directly. That said, if you provide a setter clause, you must also provide a getter clause.

和计算型属性一样，附属脚本声明支持对访问元素的读写。getter用于读取，setter用于写入。setter子句是可选的，当仅需要一个getter子句时，可以将二者都忽略，直接返回请求的值即可。也就是说，如果提供了setter子句，getter子句也必须要有。

The setter name and enclosing parentheses are optional. If you provide a setter name, it is used as the name of the parameter to the setter. If you do not provide a setter name, the default parameter name to the setter is value. That type of the setter name must be the same as the return type.

setter的名字和封闭的括号是可选的。如果提供了setter名称，它会被setter的参数名。如果没有提供setter名称，那么传给setter的参数的名称默认是value。setter名称的类型必须与返回类型(return type)的类型相同。

You can overload a subscript declaration in the type in which it is declared, as long as the parameters or the return type differ from the one you’re overloading. You can also override a subscript declaration inherited from a superclass. When you do so, you must mark the overridden subscript declaration with the override keyword.

在附属脚本声明的类型中，可以重载附属脚本，只要参数(parameters)或返回类型(return type) 与先前的不同即可。如果这样做的话，必须使用override关键字声明那个被覆盖的附属脚本。

You can also declare subscripts in the context of a protocol declaration, as described in Protocol Subscript Declaration.
在协议声明的上下文中，也声明附属脚本，正如Protocol Subscript Declaration描述的一样。

For more information about subscripting and to see examples of subscript declarations, see Subscripts。.

获取更多关于附属脚本的信息和例子，请参看Subscripts。

>GRAMMAR OF A SUBSCRIPT DECLARATION

>subscript-declaration → subscript-head­subscript-result­code-block­
>subscript-declaration → subscript-head­subscript-result­getter-setter-block­
>subscript-declaration → subscript-head­subscript-result­getter-setter-keyword-block­
>subscript-head → attributes­opt­subscript­parameter-clause­
>subscript-result → ->­attributes­opt­type­

##Operator Declaration

##运算符声明

An operator declaration introduces a new infix, prefix, or postfix operator into your program and is declared using the contextual keyword operator.

运算符声明引入了新的中缀，前缀或后缀运算到程序中，使用上下文关键字operator声明。

You can declare operators of three different fixities: infix, prefix, and postfix. The fixity of an operator specifies the relative position of an operator to its operands.

可以声明3种不同的缀：中缀、前缀和后缀。一个运算符的缀规定了一个它相对于它的操作数的相对位置。

There are three basic forms of an operator declaration, one for each fixity. The fixity of the operator is specified by including the contextual keyword infix, prefix, or postfix between operator and the name of the operator. In each form, the name of the operator can contain only the operator characters defined in Operators.

运算符声明有三种基本形式，每种缀性各一种。运算符的缀性通过在operator和运算符之间添加上下文关键字infix，prefix或postfix来指定。对于每种形式，运算符的名字只能包含Operators中定义的运算符字符。

The following form declares a new infix operator:

下面这种形式声明了一个新的中缀运算符：

> operator infix `operator name`{
    precedence `precedence level`
    associativity `associativity`
 }


An infix operator is a binary operator that is written between its two operands, such as the familiar addition operator (+) in the expression 1 + 2.

中缀运算符是二元运算符，置于两个操作数之间，比如我们熟悉的表达式1 + 2 中的加法运算符(+)。

Infix operators can optionally specify a precedence, associativity, or both.

中缀运算符可以指定优先级，结合性，或两者同时指定。

The precedence of an operator specifies how tightly an operator binds to its operands in the absence of grouping parentheses. You specify the precedence of an operator by writing the contextual keyword precedence followed by the precedence level. The precedence level can be any whole number (decimal integer) from 0 to 255; unlike decimal integer literals, it can’t contain any underscore characters. Although the precedence level is a specific number, it is significant only relative to another operator. That is, when two operators compete with each other for their operands, such as in the expression 2 + 3 * 5, the operator with the higher precedence level binds more tightly to its operands.

运算符的优先级指定了在没有分组括号的情况下，运算符与它的操作数绑定的紧密程度。可以使用上下文关键字precedence和优先等级一起来指定一个运算符的优先级。优先级可以是0到255之间的任何一个数字(十进制整数)；与十进制整数字面量不同的是，它不可以包含任何下划线字符。尽管优先级是一个特定的数字，但它仅用作与另一个运算符比较(大小)。也就是说，一个操作数可以同时被两个运算符使用时，例如2 + 3 * 5，优先级更高的运算符将优先与操作数绑定。

The associativity of an operator specifies how a sequence of operators with the same precedence level are grouped together in the absence of grouping parentheses. You specify the associativity of an operator by writing the contextual keyword associativity followed by the associativity, which is one of the contextual keywords left, right, or none. Operators that are left-associative group left-to-right. For example, the subtraction operator (-) is left-associative, and therefore the expression 4 - 5 - 6 is grouped as (4 - 5) - 6 and evaluates to -7. Operators that are right-associative group right-to-left, and operators that are specified with an associativity of none don’t associate at all. Nonassociative operators of the same precedence level can’t appear adjacent to each to other. For example, 1 < 2 < 3 is not a valid expression.

运算符的结合性明确了，没有分组的括号包围的情况下，优先级相同的运算符以何种顺序被分组的。使用上下文关键字associativity和结合性(associativity)一起来指定一个运算符的结合性，其中结合性的值是上下文关键字left，right或none之一。左结合运算符以从左到右的形式分组。例如，减法运算符(-)具有左结合性，因此表达式4 - 5 - 6以(4 - 5) - 6的形式分组，其结果为-7。 右结合运算符以从右到左的形式分组，对于设置为none的非结合运算符，它们不以任何形式分组。具有相同优先级的非结合运算符，不可以互相邻接。例如，1 < 2 < 3 就是一个无效的表达式

Infix operators that are declared without specifying a precedence or associativity are initialized with a precedence level of 100 and an associativity of none.

如果再声明时不指定任何优先级或结合性，中缀运算符的优先级会被初始化为100，结合性被初始化为none。

The following form declares a new prefix operator:

下面的形式声明了一个新的前缀运算符：

> operator prefix `operator name`{}


A prefix operator is a unary operator that is written immediately before its operand, such as the prefix increment operator (++) is in the expression ++i.

前缀运算符一元运算符，紧跟在操作数之前，比如表达式 ++i 中的前缀递增运算符(++)。

Prefix operators declarations don’t specify a precedence level. Prefix operators are nonassociative.

前缀缀运算符的声明中不指定优先级。前缀运算符是非结合的。

The following form declares a new postfix operator:

下面的形式声明了一个新的后缀运算符：


> operator postfix `operator name`{}



A postfix operator is a unary operator that is written immediately after its operand, such as the postfix increment operator (++) is in the expression i++.

后缀运算符一元运算符，紧跟在操作数之前，比如表达式 i++ 中的前后缀递增运算符(++)。

As with prefix operators, postfix operator declarations don’t specify a precedence level. Postfix operators are nonassociative.
与前缀运算符一样，后缀运算符声明不会指定优先级。后缀运算符也是非结合性的。

After declaring a new operator, you implement it by declaring a function that has the same name as the operator. To see an example of how to create and implement a new operator, see Custom Operators.

在声明了一个新的运算符止呕，要声明一个和运算符同名的函数来实现它。如何创建和实现新的操作符，请看Custom Operators。



>GRAMMAR OF AN OPERATOR DECLARATION
>
>operator-declaration → prefix-operator-declaration­  postfix-operator-declaration­  >infix-operator-declaration­
>prefix-operator-declaration → operator ­prefix­ operator­{­}­
>postfix-operator-declaration → operator ­postfix­ operator­{­}­
>infix-operator-declaration → operator­infix­operator­{­infix-operator-attributes­opt­}­
>infix-operator-attributes → precedence-clause­opt­associativity-clause­opt­
>precedence-clause → precedence­precedence-level­
>precedence-level → Digit 0 through 255
>associativity-clause → associativity­associativity­
>associativity → left­  right­  none

