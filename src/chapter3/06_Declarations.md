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




