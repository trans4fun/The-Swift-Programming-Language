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
