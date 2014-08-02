> 翻译：玩家


# 语句章节 #
----------

本页包含内容
 - [循环语句](#loop_statements)
 - [分支语句](#branch_statements)
 - [带标签的语句](#labeled_statement)
 - [控制传递语句](#control_transfer_statements)

  
在swift语言中，语句可大致分为简单语句和控制流语句两种类型的语句，简单语句是最常见的，常用来控制语句控制流语句也可分为循环语句:用来重复的执行代码块；分支语句：用来执行满足特定条件的代码块;控制语句用来决定代码的执行顺序。后续会详细阐述各控制流语句的使用。


和javascript类似，在一行语句的结束尾可以不添加分号(;)，但是如果一行有多个独立语句必须要添加。在语法上讲，在语句末尾是否添加分好都是可以的，但是从团队协助以及减少错误方面来讲，最好统一加上，一般而言大公司的svn服务器上都会添加一个钩子，用来减少出错的可能，所以最好还是养成添加的习惯。


> 语句语法  
> *语句* → [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) **;** _可选_  
> *语句* → [*声明*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/declaration) **;** _可选_  
> *语句* → [*循环语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/loop-statement) **;** _可选_  
> *语句* → [*分支语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/branch-statement) **;** _可选_  
> *语句* → [*标记语句(Labeled Statement)*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/labeled-statement)  
> *语句* → [*控制转移语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/control-transfer-statement) **;** _可选_  
> *多条语句(Statements)* → [*语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statement) [*多条语句(Statements)*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statements) _可选_  


<a name="loop_statements"></a>
##循环语句##

各个编程语言从语法上讲，基本的变量，语句都是类似的，swift循环语句也提供四种方式来循环语句：`for`语句 `for in`语句 `while`语句 `do-shile`语句
通过`break`和`continue`可以改变循环语句的控制流，和其他语言类似，具体可参考break和continue

> 循环语句语法  
> *循环语句* → [*for语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-statement)  
> *循环语句* → [*for-in语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-in-statement)  
> *循环语句* → [*while语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/while-statement)  
> *循环语句* → [*do-while语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/do-while-statement)  

##for语句##


`for`语句可以重复的执行一端代码，并且可以递增一个计数器
`for`语句的形式如下

    for `initialzation`; `condition`; `increment` {
        `statements`
    }


`initialzation` `condition`和`increment`之间的分号 不可少，`｛`也不可少

 1. `initialzation`只是被执行一次，通常用于声明和初始化在接下来循环中需要的变量
 2. `condition`：如果为真（`true`）`statements`将会执行，进行第3步，如果为`false`则`statements`和`increment`都不会被执行，for至此执行完毕
 3. 计算`increment`表达式，然后转到第2步。
 
定义在`initialzation`中的变量仅在`for`语句的作用域以内有效。`condition`表达式的值的类型必须遵循LogicValue协议。

> For 循环语法  
> *for语句* → for [*for初始条件*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-init) _可选_ **;** [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) _可选_ **;** [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) _可选_ [*代码块*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block)  
> for语句 → for  [*for初始条件*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-init) _可选_ **;** [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) _可选_ **;** [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) _可选_ **)** [*代码块*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block)  
> *for初始条件* → [*变量声明*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/variable-declaration) | [*表达式列表*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression-list) 


##For-In 语句##


`for-in`语句允许在重复执行代码块的同时，迭代集合(或遵循Sequence协议的任意类型)中的每一项。

`for-in`语句的形式如下：

    for `item` in `collection` {
        `statements`
    }
    


`for-in`语句在循环开始前会调用`collection`表达式的`generate`方法来获取一个生成器类型（这是一个遵循Generator协议的类型）的值。接下来循环开始，调用`collection`表达式的`next`方法。如果其返回值不是`None`，它将会被赋给`item`，然后执行`statements`，执行完毕后回到循环开始处；否则，将不会赋值给`item`也不会执行`statements`，`for-in`至此执行完毕。这和`javascript`中的`for in`语句是一样的，可以理解为循环`collection`，如果有key的取出，去执行接下来的`statements`

`For-In`循环语法  
> *for-in语句* → **for** [*模式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Patterns.html#//apple_ref/swift/grammar/pattern) **in** [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) [*代码块*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block) 

##While语句##

`while`语句允许重复执行代码块
`while`语句的形式如下：

    while `condition` {
        `statements`
    }

    
`while`语句的执行流程为判断`condition`，如果为真(`true`),这会执行`statements`,否则`while`语句执行到此结束
由于`condition`的值在`statements`执行前就已计算出，因此`while`语句中的`statements`可能会被执行若干次，也可能不会被执行。
`condition`表达式的值的类型必须遵循LogicValue协议。同时，`condition`表达式也可以使用可选绑定，请参考可选绑定待添加链接。

> While 循环语法  
> *while语句* → **while** [*while-condition*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/while-condition) [*code-block*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)  
> *while条件* → [*expression*](..\chapter3\04_Expressions.html#expression) | [*declaration*](..\chapter3\05_Declarations.html#declaration)  


##Do-While 语句##


`do-while`语句允许代码块被执行一次或多次。
`do-while`语句的形式如下：

    do {
        `statements`
    } while `condition`
    

`do-while`语句的执行流程如下:

 1. 执行`statements`，完后钻到2
 2. 计算condition表达式，如果返回（`true`）继续回到1新一轮执行，否则`do-while`至此执行完毕


 由于`condition`是在`statements`执行之后才会计算，因此可见，相比较`while`而言，`do-while`至少会执行一次
`condition`表达式的值的类型必须遵循`LogicValue`协议。同时，`condition`表达式也可以使用可选绑定，请参考可选绑定。
> do-while-statement→ do [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block) while [while-condition](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/while-condition)


<a name="branch_statements"></a>
##分支语句##

通过一个或者多个条件的值，来决定语句允许程序执行指定部分的代码，swift和其他语言类似提供了`if`语句和`switch`语句
`switch`语句中的控制流可以用`break`语句修改，请参考[Break](http://chinaz.com/swift/chapter3/10_Statements.html#break_statement) 语句。
>branch-statement → [if-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-statement)
>branch-statement → [switch-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-statement)

##if语句##

通过一个或多个条件的值来决定执行哪一块的代码，if语句主要有三种使用方式，但无乱哪种方式都需要添加`{`和`}`
第一种形式是当且仅当条件为真时执行代码，像下面这样：

    if `condition` {
        `statements`
    }
    
 
第二种形式是在第一种形式的基础上添加else语句，当只有一个else语句时，像下面这样：

    if `condition` {
        `statements to execute if condition is true`
    } else {
        `statements to execute if condition is false`
    }
    
第三种则是else中又需要进行判断，即有多种判断情况：

    if `condition 1` {
        `statements to execute if condition 1 is true`
    } else if `condition 2` {
        `statements to execute if condition 2 is true`
    }
    else {
        `statements to execute if both conditions are false`
    }


`if`语句中条件的值的类型必须遵循`LogicValue`协议。同时，条件也可以使用可选绑定，请参考可选绑定`待添加链接`
>if-statement → if [if-condition](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-condition) [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-condition) [else-clause](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/else-clause) opt

>if-condition → [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) | [declaration](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/declaration)

>else-clause → else [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block) | else [if-statement opt](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-statement)

##Switch 语句##

取决于`switch~语句的控制表达式(control expression)，`switch`语句将决定执行哪一块代码。

switch语句的形式如下：

    switch `control expression` {
        case `pattern 1`:
            `statements`
        case `pattern 2` where `condition`:
            `statements`
        case `pattern 3` where `condition`,
        `pattern 4` where `condition`:
            `statements`
        default:
            `statements`
    }

`switch`语句的表达式`control expression`会首选被计算，然后与下面的每个`case`的模式进行匹配，如果匹配成功，程序将会执行对应`case`中的`statements`,需要注意的是每个case不能为空，也就是说在case中至少有一条语句，如果在相应case中不想执行代码，只需要在程序中写个`break`即可

case let (x, y) where x == y:

可以用作控制表达式的值是什么灵活的，除了标量类型(scalartypes,如`Int`、`Character`)之外，你还可以使用其他任何类型的值，包括浮点数，字符串，远组，自定义类的实例以及可选(`optional`)类型，甚至是枚举类型中的成员和指定的范围(`range`)等。关于在`switch`语句中使用这些类型，请参考控制流章节的Switch.

你可以在模式后端添加一个保护作用的表达式(guard expression)，构成是这样的:关键字`where`后面跟着一个作为额外测试条件的表达式，因此当且仅当表达式匹配的一个case的某个模式在保护作用的表达式为真时，对应case中的`statements`才会被执行，在下面例子中，控制表达式只会匹配含有两个相等元素的元组

    case let (x, y) where x == y:
    }


正如上面的例子，也可以在模式中使用let（或var）语句来绑定常量（或变量）。这些常量（或变量）可以在其对应的起保护作用的表达式和其对应的case块里的代码中引用。但是，如果case中有多个模式匹配控制表达式，那么这些模式都不能绑定常量（或变量）。


switch语句也可以包含默认(default)块，只有其它case块都无法匹配控制表达式时，默认块中的代码才会被执行。一个switch语句只能有一个默认块，而且必须在switch语句的最后面。

尽管模式匹配操作的实际执行顺序，并且计算顺序是不可知的，但是Swift规定能够了swift中的语句中的模式匹配顺序和书写源码的顺序保持一致。因此，当多个模式含有相通的值并且能够匹配控制表达式时，程序只会执行源码中第一个匹配`case`中的代码

##Switch 语句必须是完备的##

`switch`语句中包含多个`case`,每个`case`都是`switch`的一个分支，由`switch`来决定执行哪一个分支代码，`switch`语句必须是完整的，也就是值必须与`case`中的某一个对应，可以通过`default`来指定默认就不符合`case`条件时执行的代码块，并且这个`default`分支必须在最后。

##不存在隐式的贯穿(fall through)##

当匹配的`case`代码在执行完毕后，程序会终止`switch`语句，而不会继续执行下一个`case`语句，这就意味着，如果你想执行下一个case块，需要显式地在你需要的case块里使用fallthrough语句。关于fallthrough语句的更多信息，请参考Fallthrough 语句。

> switch-statement -> switch [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) {[switch-cases](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-cases) opt}
> switch-cases -> [switch-case](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-case) [switch-cases](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-cases) opt
> switch-case -> [case-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/case-label) [statements](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statements) | [default-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/default-label) [statements](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statements)
> switch-case [switch-case](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/case-label): | [default-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/default-label):
> case-label -> case [case-item-list](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/case-item-list):
> case-item-list -> [pattern](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Patterns.html#//apple_ref/swift/grammar/pattern)   [guard-clause](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/guard-clause) opt | [pattern](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Patterns.html#//apple_ref/swift/grammar/pattern) [guard-clause](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/guard-clause)opt , [case-item-list](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/case-item-list)
> default-label -> default
> guard-clause -> where [guard-expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/guard-expression)
> guard-expression -> [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)

<a name="labeled_statement"></a>
##带标签的语句##

你可以在循环语句和`switch`语句前面加上标签，它由标签名和`：`组成，在`break`和`continue`后面跟上标签名可以显式的在循环语句和switch语句中更改控制流，把控制权传递给指定标签标记的语句。关于这两条语句用法，请参考[Break](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/doc/uid/TP40014097-CH33-XID_976) 语句和[Continue](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/doc/uid/TP40014097-CH33-XID_976) 语句


标签的作用域是该标签所标记的语句之后的所有语句。你可以不使用带标签的语句，但只要使用它，标签名就必唯一。

关于使用带标签的语句的例子，请参考控制流一章的带标签的语句

> labeld-statement -> [statement-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statement-label) [loop-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/loop-statement) | [statement-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statement-label) [switch-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-statement)
> statement-label -> [label-name](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/label-name):
> label-name -> [identifier](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier)

<a name="control_transfer_statements"></a>
##控制传递语句##

能够无条件的把控制权从一片代码传递到另一片代码，控制传递语句能够改变代码的执行顺序，Swift 提供四种类型的控制传递语句： `break`语句，`continue`语句，`fallthrough`语句和`return`语句

> control-transfer-statement -> [break-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/break-statement)
> control-transfer-statement -> [continue-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/continue-statement)
> continue-statement -> [fallthrougth-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/fallthrough-statement)
> continue-statement -> [return-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/return-statement)

##break语句##

`break`用于终止循环或是`switch`语句，用break语句时，可以只写break这个关键词，也可以在break后面跟上标签名(label name)，像下面这样：

    break
    break label name
    

当`break`后面带有标签名时，可用于终止这个标签标记的循环或`switch`语句的执行

而当只有`break`关键词时，则会终止`switch`语句或上下文中包含`break`
的最内层的循环的执行

在这两种情况下，控制权都会被传递给循环或switch语句外面的第一行语句

关于使用break语句的例子，请参考控制流一章的Break和带标签的语句

> break-statement -> break [label-name](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/label-name) opt

##Continue 语句##

continue语句用于终止循环中当前迭代的执行，但不会终止该循环的执行。使用continue语句时，和break一样，可以只写continue这个关键词，也可以在continue后面跟上标签名(label name)，像下面这样：

    continue
    continue label name
    

当continue语句后面带标签名时，可用于终止由这个标签标记的循环中当前迭代的执行

而当只写break时，可用于终止上下文中包含continue语句的最内层循环中当前迭代的执行

在这两种情况下，控制权都会被传递给循环外面的第一行语句。

在for语句中，continue语句执行后，increment表达式还是会被计算，这是因为每次循环体执行完毕后increment表达式都会被计算。

关于使用continue语句的例子，请参考控制流一章的Continue和带标签的语句

> continue-statement -> continue [label-name](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/label-name)opt


##Fallthrough 语句##

`fallthrough`语句用于在`switch`语句中传递控制权。`fallthrough`语句会把控制权从`switch`语句中的一个`case`无条件的传递给下一个case，即使下一个`case`的值与`switch`语句的控制表达式的值不匹配

关于在switch语句中使用fallthrough语句的例子，请参考控制流一章的控制传递语句

> fallthrough-statement -> fallthrough

##Return 语句##

`return`用于在函数或是方法中，将控制权传递给调用者，接着程序将会从调用者的位置继续的往下执行
使用return语句时，可以只写return这个关键词，也可以在return后面跟上表达式，像下面这样

    return
    return `expression`
    

当`return`后面跟有表达式时，会把表达式的值返回给调用者，如果表达式值的类型与调用者期望的类型不匹配，swift会在返回表达式的值之前把表达式值的类型转为调用者期望的类型

而当只写return时，仅仅是将控制权从该函数或方法传递给调用者，而不返回一个值。（这就是说，该函数或方法的返回类型为Void或()）

> return-statement -> return [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)opt
