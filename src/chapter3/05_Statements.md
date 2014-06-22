> 翻译：玩家


#Statements#
---------
# 语句章节 #
----------

本页包含内容
 - [循环语句](#loop_statements)
 - [分支语句](#branch_statements)
 - [带标签的语句](#labeled_statement)
 - [控制传递语句](#control_transfer_statements)

In Swift, there are two kinds of statements: simple statements and control flow statements. Simple statements are the most common and consist of either an expression or a declaration. Control flow statements are used to control the flow of execution in a program. There are three types of control flow statements in Swift: loop statements, branch statements, and control transfer statements.
  
swift和其他语言一样，语句可大致分为简单语句和控制流语句，控制流语句也可分为循环语句:用来重复的执行代码块；分支语句：用来执行满足特定条件的代码块;控制语句用来决定代码的执行顺序。后续会详细阐述各控制流语句的使用。

Loop statements allow a block of code to be executed repeatedly, branch statements allow a certain block of code to be executed only when certain conditions are met, and control transfer statements provide a way to alter the order in which code is executed. Each type of control flow statement is described in detail below.

A semicolon (;) can optionally appear after any statement and is used to separate multiple statements if they appear on the same line.

和javascript类似，在一行语句的结束尾可以不添加分号(;)，但是如果一行有多个独立语句必须要添加。在语法上讲，在语句末尾是否添加分好都是可以的，但是从团队协助以及减少错误方面来讲，最好统一加上，一般而言大公司的svn服务器上都会添加一个钩子，用来减少出错的可能，所以最好还是养成添加的习惯。

> statement -> [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)；opt
> statement -> [declaration](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/declaration)；opt
> statement -> [loop-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/loop-statement);opt
> statement -> [branch-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/branch-statement);opt
> statement -> [labeled-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/branch-statement)
> statement -> [control-transfer-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/control-transfer-statement);opt
> statement -> [statement statements](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/control-transfer-statement);opt

 
 ---------


> 语句语法  
> *语句* → [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) **;** _可选_  
> *语句* → [*声明*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/declaration) **;** _可选_  
> *语句* → [*循环语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/loop-statement) **;** _可选_  
> *语句* → [*分支语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/branch-statement) **;** _可选_  
> *语句* → [*标记语句(Labeled Statement)*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/labeled-statement)  
> *语句* → [*控制转移语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/control-transfer-statement) **;** _可选_  
> *多条语句(Statements)* → [*语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statement) [*多条语句(Statements)*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statements) _可选_  


<a name="loop_statements"></a>
##Loop Statements##
##循环语句##

Loop statements allow a block of code to be executed repeatedly, depending on the conditions specified in the loop. Swift has four loop statements: a for statement, a for-in statement, a while statement, and a do-while statement.

Control flow in a loop statement can be changed by a break statement and a continue statement and is discussed in Break Statement and Continue Statement below.

> loop-statement -> [for-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-statement)
> loop-statement -> [for-in-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-in-statement)
> loop-statement -> [while-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/while-statement)
> loop-statement -> [do-while-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/do-while-statement)

各个编程语言从语法上讲，基本的变量，语句都是类似的，swift循环语句也提供四种方式来循环语句：`for`语句 `for in`语句 `while`语句 `do-shile`语句
通过`break`和`continue`可以改变循环语句的控制流，和其他语言类似，具体可参考break和continue

> 循环语句语法  
> *循环语句* → [*for语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-statement)  
> *循环语句* → [*for-in语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-in-statement)  
> *循环语句* → [*while语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/while-statement)  
> *循环语句* → [*do-while语句*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/do-while-statement)  


##For Statement##
##for语句##

A for statement allows a block of code to be executed repeatedly while incrementing a counter, as long as a condition remains true.

A for statement has the following form:

    for initialization; condition; increment {
        statements
    }

`for`语句可以重复的执行一端代码，并且可以递增一个计数器
`for`语句的形式如下

    for `initialzation`; `condition`; `increment` {
        `statements`
    }
    
The semicolons between the initialization, condition, and increment are required. The braces around the statements in the body of the loop are also required.

A for statement is executed as follows:

The initialization is evaluated only once. It is typically used to declare and initialize any variables that are needed for the remainder of the loop.
The condition expression is evaluated.
If true, the program executes the statements, and execution continues to step 3. If false, the program does not execute the statements or the increment expression, and the program is finished executing the for statement.
The increment expression is evaluated, and execution returns to step 2.
Variables defined within the initialization are valid only within the scope of the for statement itself.

The value of the condition expression must have a type that conforms to the LogicValue protocol.

> for-statement -> for [for-init](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-init)；[expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)opt; [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)opt [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block)
> for-statement -> for ([for-init](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-init)opt;[expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)opt; [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)opt) [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block)
> for-init -> [variable-declaration](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/variable-declaration) | [expression-list](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression-list)


`initialzation` `condition`和`increment`之间的分号 不可少，`｛`也不可少

 1. `initialzation`只是被执行一次，通常用于声明和初始化在接下来循环中需要的变量
 2. `condition`：如果为真（`true`）`statements`将会执行，进行第3步，如果为`false`则`statements`和`increment`都不会被执行，for至此执行完毕
 3. 计算`increment`表达式，然后转到第2步。
 
定义在`initialzation`中的变量仅在`for`语句的作用域以内有效。`condition`表达式的值的类型必须遵循LogicValue协议。

> For 循环语法  
> *for语句* → for [*for初始条件*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-init) _可选_ **;** [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) _可选_ **;** [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) _可选_ [*代码块*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block)  
> for语句 → for  [*for初始条件*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/for-init) _可选_ **;** [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) _可选_ **;** [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) _可选_ **)** [*代码块*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block)  
> *for初始条件* → [*变量声明*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/variable-declaration) | [*表达式列表*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression-list) 


##For-In Statement##
##For-In 语句##

A for-in statement allows a block of code to be executed once for each item in a collection (or any type) that conforms to the Sequence protocol.

A for-in statement has the following form:

    for item in collection {
        statements
    }

`for-in`语句允许在重复执行代码块的同时，迭代集合(或遵循Sequence协议的任意类型)中的每一项。

`for-in`语句的形式如下：

    for `item` in `collection` {
        `statements`
    }
    
The generate method is called on the collection expression to obtain a value of a generator type—that is, a type that conforms to the Generator protocol. The program begins executing a loop by calling the next method on the stream. If the value returned is not None, it is assigned to the item pattern, the program executes the statements, and then continues execution at the beginning of the loop. Otherwise, the program does not perform assignment or execute the statements, and it is finished executing the for-in statement

> GRAMMAR OF A FOR-IN STATEMENT
> for-in-statement -> for [pattern](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Patterns.html#//apple_ref/swift/grammar/pattern) in [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block)

`for-in`语句在循环开始前会调用`collection`表达式的`generate`方法来获取一个生成器类型（这是一个遵循Generator协议的类型）的值。接下来循环开始，调用`collection`表达式的`next`方法。如果其返回值不是`None`，它将会被赋给`item`，然后执行`statements`，执行完毕后回到循环开始处；否则，将不会赋值给`item`也不会执行`statements`，`for-in`至此执行完毕。这和`javascript`中的`for in`语句是一样的，可以理解为循环`collection`，如果有key的取出，去执行接下来的`statements`

`For-In`循环语法  
> *for-in语句* → **for** [*模式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Patterns.html#//apple_ref/swift/grammar/pattern) **in** [*表达式*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) [*代码块*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block) 


##While Statement##
##While语句##

A while statement allows a block of code to be executed repeatedly, as long as a condition remains true.

A while statement has the following form:

    while condition {
        statements
    }

`while`语句允许重复执行代码块
`while`语句的形式如下：

    while `condition` {
        `statements`
    }
    
A while statement is executed as follows:

 1. The condition is evaluated.
If true, execution continues to step 2. If false, the program is finished executing the while statement.
 2. The program executes the statements, and execution returns to step 1.

Because the value of the condition is evaluated before the statements are executed, the statements in a while statement can be executed zero or more times.

The value of the condition must have a type that conforms to the LogicValue protocol. The condition can also be an optional binding declaration, as discussed in [Optional Bindind](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html#//apple_ref/doc/uid/TP40014097-CH5-XID_432)

> GRAMMAR OF A WHILE STATEMENT
> while-statement -> whild [while-condition](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/while-condition) [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block)
> while-condition -> [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) | [declaration](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/declaration)
 
    
`while`语句的执行流程为判断`condition`，如果为真(`true`),这会执行`statements`,否则`while`语句执行到此结束
由于`condition`的值在`statements`执行前就已计算出，因此`while`语句中的`statements`可能会被执行若干次，也可能不会被执行。
`condition`表达式的值的类型必须遵循LogicValue协议。同时，`condition`表达式也可以使用可选绑定，请参考可选绑定待添加链接。

> While 循环语法  
> *while语句* → **while** [*while-condition*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/while-condition) [*code-block*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)  
> *while条件* → [*expression*](..\chapter3\04_Expressions.html#expression) | [*declaration*](..\chapter3\05_Declarations.html#declaration)  


##Do-While Statement##
##Do-While 语句##

A do-while statement allows a block of code to be executed one or more times, as long as a condition remains true.

A do-while statement has the following form:

    do {
        statements
    } while condition

`do-while`语句允许代码块被执行一次或多次。
`do-while`语句的形式如下：

    do {
        `statements`
    } while `condition`
    
A do-while statement is executed as follows:

 1. The program executes the statements, and execution continues to step 2
 2. The condition is evaluated.If true, execution returns to step 1. If false, the program is finished executing the do-while statement.

`do-while`语句的执行流程如下:

 1. 执行`statements`，完后钻到2
 2. 计算condition表达式，如果返回（`true`）继续回到1新一轮执行，否则`do-while`至此执行完毕

Because the value of the condition is evaluated after the statements are executed, the statements in a do-while statement are executed at least once.

The value of the condition must have a type that conforms to the LogicValue protocol. The condition can also be an optional binding declaration, as discussed in [Optional Binding](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html#//apple_ref/doc/uid/TP40014097-CH5-XID_432)

 由于`condition`是在`statements`执行之后才会计算，因此可见，相比较`while`而言，`do-while`至少会执行一次
`condition`表达式的值的类型必须遵循`LogicValue`协议。同时，`condition`表达式也可以使用可选绑定，请参考可选绑定。
> do-while-statement→ do [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block) while [while-condition](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/while-condition)


<a name="branch_statements"></a>
##Branch Statements##
##分支语句##

Branch statements allow the program to execute certain parts of code depending on the value of one or more conditions. The values of the conditions specified in a branch statement control how the program branches and, therefore, what block of code is executed. Swift has two branch statements: an if statement and a switch statement.

Control flow in a switch statement can be changed by a break statement and is discussed in Break Statement below

> GRAMMAR OF A BRANCH STAREMENT
> branch-statement -> [if-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-statement)
> brach-statement -> [switch-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-statement)

通过一个或者多个条件的值，来决定语句允许程序执行指定部分的代码，swift和其他语言类似提供了`if`语句和`switch`语句
`switch`语句中的控制流可以用`break`语句修改，请参考[Break](http://chinaz.com/swift/chapter3/10_Statements.html#break_statement) 语句。
>branch-statement → [if-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-statement)
>branch-statement → [switch-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-statement)


##If Statement##
##if语句##

An if statement is used for executing code based on the evaluation of one or more conditions.

There are two basic forms of an if statement. In each form, the opening and closing braces are required.

The first form allows code to be executed only when a condition is true and has the following form:

    if condition {
        statements
    }

通过一个或多个条件的值来决定执行哪一块的代码，if语句主要有三种使用方式，但无乱哪种方式都需要添加`{`和`}`
第一种形式是当且仅当条件为真时执行代码，像下面这样：

    if `condition` {
        `statements`
    }
    
The second form of an if statement provides an additional else clause (introduced by the else keyword) and is used for executing one part of code when the condition is true and another part code when the same condition is false. When a single else clause is present, an if statement has the following form:
 

    if condition {
        statements to execute if condition is true
    } else {
        statements to execute if condition is false
    }

The else clause of an if statement can contain another if statement to test more than one condition. An if statement chained together in this way has the following form:

    if condition 1 {
        statements to execute if condition 1 is true
    } else if condition 2 {
        statements to execute if condition 2 is true
    } else {
        statements to execute if both conditions are false
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
    
The value of any condition in an if statement must have a type that conforms to the LogicValue protocol. The condition can also be an optional binding declaration, as discussed in[Option Binding](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html#//apple_ref/doc/uid/TP40014097-CH5-XID_432)

> GRAMMAR OF AN IF STATEMENT
> if-statement -> if [if-condition](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-condition) [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block) [else-clause](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/else-clause) opt
> if-condition -> [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) | [declaration](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/declaration)
> else-clause -> else [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block) | else [if-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-statement)


`if`语句中条件的值的类型必须遵循`LogicValue`协议。同时，条件也可以使用可选绑定，请参考可选绑定`待添加链接`
>if-statement → if [if-condition](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-condition) [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-condition) [else-clause](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/else-clause) opt

>if-condition → [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) | [declaration](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/declaration)

>else-clause → else [code-block](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Declarations.html#//apple_ref/swift/grammar/code-block) | else [if-statement opt](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/if-statement)


##Switch Statement##
##Switch 语句##

A switch statement allows certain blocks of code to be executed depending on the value of a control expression.
A switch statement has the following form:

    switch control expression {
    case pattern 1:
        statements
    case pattern 2 where condition:
        statements
    case pattern 3 where condition,
    pattern 4 where condition:
        statements
    default:
        statements
    }

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
The control expression of the switch statement is evaluated and then compared with the patterns specified in each case. If a match is found, the program executes the statements listed within the scope of that case. The scope of each case can’t be empty. As a result, you must include at least one statement following the colon (:) of each case label. Use a single break statement if you don’t intend to execute any code in the body of a matched case.

`switch`语句的表达式`control expression`会首选被计算，然后与下面的每个`case`的模式进行匹配，如果匹配成功，程序将会执行对应`case`中的`statements`,需要注意的是每个case不能为空，也就是说在case中至少有一条语句，如果在相应case中不想执行代码，只需要在程序中写个`break`即可


The values of expressions your code can branch on is very flexible. For instance, in addition to the values of scalar types, such as integers and characters, your code can branch on the values of any type, including floating-point numbers, strings, tuples, instances of custom classes, and optionals. The value of the control expression can even be matched to the value of a case in an enumeration and checked for inclusion in a specified range of values. For examples of how to use these various types of values in switch statements, see Switch in the Control Flow chapter.

A switch case can optionally contain a guard expression after each pattern. A guard expression is introduced by the keyword where followed by an expression, and is used to provide an additional condition before a pattern in a case is considered matched to the control expression. If a guard expression is present, the statements within the relevant case are executed only if the value of the control expression matches one of the patterns of the case and the guard expression evaluates to true. For instance, a control expression matches the case in the example below only if it is a tuple that contains two elements of the same value, such as (1, 1).

case let (x, y) where x == y:

可以用作控制表达式的值是什么灵活的，除了标量类型(scalartypes,如`Int`、`Character`)之外，你还可以使用其他任何类型的值，包括浮点数，字符串，远组，自定义类的实例以及可选(`optional`)类型，甚至是枚举类型中的成员和指定的范围(`range`)等。关于在`switch`语句中使用这些类型，请参考控制流章节的Switch.

你可以在模式后端添加一个保护作用的表达式(guard expression)，构成是这样的:关键字`where`后面跟着一个作为额外测试条件的表达式，因此当且仅当表达式匹配的一个case的某个模式在保护作用的表达式为真时，对应case中的`statements`才会被执行，在下面例子中，控制表达式只会匹配含有两个相等元素的元组

    case let (x, y) where x == y:
    }


As the above example shows, patterns in a case can also bind constants using the keyword let (they can also bind variables using the keyword var). These constants (or variables) can then be referenced in a corresponding guard expression and throughout the rest of the code within the scope of the case. That said, if the case contains multiple patterns that match the control expression, none of those patterns can contain constant or variable bindings.


正如上面的例子，也可以在模式中使用let（或var）语句来绑定常量（或变量）。这些常量（或变量）可以在其对应的起保护作用的表达式和其对应的case块里的代码中引用。但是，如果case中有多个模式匹配控制表达式，那么这些模式都不能绑定常量（或变量）。

A switch statement can also include a default case, introduced by the keyword default. The code within a default case is executed only if no other cases match the control expression. A switch statement can include only one default case, which must appear at the end of the switch statement.

Although the actual execution order of pattern-matching operations, and in particular the evaluation order of patterns in cases, is unspecified, pattern matching in a switch statement behaves as if the evaluation is performed in source order—that is, the order in which they appear in source code. As a result, if multiple cases contain patterns that evaluate to the same value, and thus can match the value of the control expression, the program executes only the code within the first matching case in source order.

switch语句也可以包含默认(default)块，只有其它case块都无法匹配控制表达式时，默认块中的代码才会被执行。一个switch语句只能有一个默认块，而且必须在switch语句的最后面。

尽管模式匹配操作的实际执行顺序，并且计算顺序是不可知的，但是Swift规定能够了swift中的语句中的模式匹配顺序和书写源码的顺序保持一致。因此，当多个模式含有相通的值并且能够匹配控制表达式时，程序只会执行源码中第一个匹配`case`中的代码

##Switch Statements Must Be Exhaustive##
##Switch 语句必须是完备的##

In Swift, every possible value of the control expression’s type must match the value of at least one pattern of a case. When this simply isn’t feasible (for instance, when the control expression’s type is Int), you can include a default case to satisfy the requirement

`switch`语句中包含多个`case`,每个`case`都是`switch`的一个分支，由`switch`来决定执行哪一个分支代码，`switch`语句必须是完整的，也就是值必须与`case`中的某一个对应，可以通过`default`来指定默认就不符合`case`条件时执行的代码块，并且这个`default`分支必须在最后。

##Execution Does Not Fall Through Cases Implicitly##
##不存在隐式的贯穿(fall through)##

After the code within a matched case has finished executing, the program exits from the switch statement. Program execution does not continue or “fall through” to the next case or default case. That said, if you want execution to continue from one case to the next, explicitly include a fallthrough statement, which simply consists of the keyword fallthrough, in the case from which you want execution to continue. For more information about the fallthrough statement, see Fallthrough Statement below

> switch-statement -> switch [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression) {[switch-cases](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-cases) opt}
> switch-cases -> [switch-case](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-case) [switch-cases](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-cases) opt
> switch-case -> [case-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/case-label) [statements](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statements) | [default-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/default-label) [statements](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statements)
> switch-case [switch-case](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/case-label): | [default-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/default-label):
> case-label -> case [case-item-list](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/case-item-list):
> case-item-list -> [pattern](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Patterns.html#//apple_ref/swift/grammar/pattern)   [guard-clause](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/guard-clause) opt | [pattern](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Patterns.html#//apple_ref/swift/grammar/pattern) [guard-clause](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/guard-clause)opt , [case-item-list](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/case-item-list)
> default-label -> default
> guard-clause -> where [guard-expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/guard-expression)
> guard-expression -> [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)

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
##Labeled Statement##
##带标签的语句##

You can prefix a loop statement or a switch statement with a statement label, which consists of the name of the label followed immediately by a colon (:). Use statement labels with break and continue statements to be explicit about how you want to change control flow in a loop statement or a switch statement, as discussed in Break Statement and Continue Statement below.

你可以在循环语句和`switch`语句前面加上标签，它由标签名和`：`组成，在`break`和`continue`后面跟上标签名可以显式的在循环语句和switch语句中更改控制流，把控制权传递给指定标签标记的语句。关于这两条语句用法，请参考[Break](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/doc/uid/TP40014097-CH33-XID_976) 语句和[Continue](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/doc/uid/TP40014097-CH33-XID_976) 语句

The scope of a labeled statement is the entire statement following the statement label. You can nest labeled statements, but the name of each statement label must be unique.

For more information and to see examples of how to use statement labels, see Labeled Statements in the Control Flow chapter

> labeld-statement -> [statement-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statement-label) [loop-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/loop-statement) | [statement-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statement-label) [switch-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-statement)
> statement-label -> [label-name](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/label-name):
> label-name -> [identifier](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier)



标签的作用域是该标签所标记的语句之后的所有语句。你可以不使用带标签的语句，但只要使用它，标签名就必唯一。

关于使用带标签的语句的例子，请参考控制流一章的带标签的语句

> labeld-statement -> [statement-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statement-label) [loop-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/loop-statement) | [statement-label](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/statement-label) [switch-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/switch-statement)
> statement-label -> [label-name](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/label-name):
> label-name -> [identifier](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/swift/grammar/identifier)

<a name="control_transfer_statements"></a>
##Control Transfer Statements##
##控制传递语句##

Control transfer statements can change the order in which code in your program is executed by unconditionally transferring program control from one piece of code to another. Swift has four control transfer statements: a break statement, a continue statement, a fallthrough statement, and a return statement.

> control-transfer-statement -> [break-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/break-statement)
> control-transfer-statement -> [continue-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/continue-statement)
> continue-statement -> [fallthrougth-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/fallthrough-statement)
> continue-statement -> [return-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/return-statement)

能够无条件的把控制权从一片代码传递到另一片代码，控制传递语句能够改变代码的执行顺序，Swift 提供四种类型的控制传递语句： `break`语句，`continue`语句，`fallthrough`语句和`return`语句

> control-transfer-statement -> [break-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/break-statement)
> control-transfer-statement -> [continue-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/continue-statement)
> continue-statement -> [fallthrougth-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/fallthrough-statement)
> continue-statement -> [return-statement](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/return-statement)

##Break Statement##
##bream语句##
A break statement ends program execution of a loop or a switch statement. A break statement can consist of only the keyword break, or it can consist of the keyword break followed by the name of a statement label, as shown below.

    break
    break label name
    
`break`用于终止循环或是`switch`语句，用break语句时，可以只写break这个关键词，也可以在break后面跟上标签名(label name)，像下面这样：

    break
    break label name
    
When a break statement is followed by the name of a statement label, it ends program execution of the loop or switch statement named by that label.

When a break statement is not followed by the name of a statement label, it ends program execution of the switch statement or the innermost enclosing loop statement in which it occurs.

当`break`后面带有标签名时，可用于终止这个标签标记的循环或`switch`语句的执行

而当只有`break`关键词时，则会终止`switch`语句或上下文中包含`break`
的最内层的循环的执行

In both cases, program control is then transferred to the first line of code following the enclosing loop or switch statement, if any.

For examples of how to use a break statement, see Break and Labeled Statements in the Control Flow chapter.

> break-statement -> break [label-name](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/label-name) opt

在这两种情况下，控制权都会被传递给循环或switch语句外面的第一行语句

关于使用break语句的例子，请参考控制流一章的Break和带标签的语句

> break-statement -> break [label-name](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/label-name) opt

##Continue Statement##
##Continue 语句##
A continue statement ends program execution of the current iteration of a loop statement but does not stop execution of the loop statement. A continue statement can consist of only the keyword continue, or it can consist of the keyword continue followed by the name of a statement label, as shown below.

    continue
    continue label name
    
continue语句用于终止循环中当前迭代的执行，但不会终止该循环的执行。使用continue语句时，和break一样，可以只写continue这个关键词，也可以在continue后面跟上标签名(label name)，像下面这样：

    continue
    continue label name
    
When a continue statement is followed by the name of a statement label, it ends program execution of the current iteration of the loop statement named by that label.

When a continue statement is not followed by the name of a statement label, it ends program execution of the current iteration of the innermost enclosing loop statement in which it occurs.

当continue语句后面带标签名时，可用于终止由这个标签标记的循环中当前迭代的执行

而当只写break时，可用于终止上下文中包含continue语句的最内层循环中当前迭代的执行

In both cases, program control is then transferred to the condition of the enclosing loop statement.

In a for statement, the increment expression is still evaluated after the continue statement is executed, because the increment expression is evaluated after the execution of the loop’s body.

For examples of how to use a continue statement, see Continue and Labeled Statements in the Control Flow chapter

> continue-statement -> continue [label-name](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/label-name)opt

在这两种情况下，控制权都会被传递给循环外面的第一行语句。

在for语句中，continue语句执行后，increment表达式还是会被计算，这是因为每次循环体执行完毕后increment表达式都会被计算。

关于使用continue语句的例子，请参考控制流一章的Continue和带标签的语句

> continue-statement -> continue [label-name](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Statements.html#//apple_ref/swift/grammar/label-name)opt


##Fallthrough Statement##
##Fallthrough 语句##

A fallthrough statement consists of the fallthrough keyword and occurs only in a case block of a switch statement. A fallthrough statement causes program execution to continue from one case in a switch statement to the next case. Program execution continues to the next case even if the patterns of the case label do not match the value of the switch statement’s control expression.

A fallthrough statement can appear anywhere inside a switch statement, not just as the last statement of a case block, but it can’t be used in the final case block. It also cannot transfer control into a case block whose pattern contains value binding patterns.

`fallthrough`语句用于在`switch`语句中传递控制权。`fallthrough`语句会把控制权从`switch`语句中的一个`case`无条件的传递给下一个case，即使下一个`case`的值与`switch`语句的控制表达式的值不匹配

For an example of how to use a fallthrough statement in a switch statement, see Control Transfer Statements in the Control Flow chapter.

> fallthrough-statement -> fallthrough

关于在switch语句中使用fallthrough语句的例子，请参考控制流一章的控制传递语句

> fallthrough-statement -> fallthrough

##Return Statement##
##Return 语句##

A return statement occurs only in the body of a function or method definition and causes program execution to return to the calling function or method. Program execution continues at the point immediately following the function or method call.

A return statement can consist of only the keyword return, or it can consist of the keyword return followed by an expression, as shown below.

    return
    return expression
    
`return`用于在函数或是方法中，将控制权传递给调用者，接着程序将会从调用者的位置继续的往下执行
使用return语句时，可以只写return这个关键词，也可以在return后面跟上表达式，像下面这样

    return
    return `expression`
    
When a return statement is followed by an expression, the value of the expression is returned to the calling function or method. If the value of the expression does not match the value of the return type declared in the function or method declaration, the expression’s value is converted to the return type before it is returned to the calling function or method.

当`return`后面跟有表达式时，会把表达式的值返回给调用者，如果表达式值的类型与调用者期望的类型不匹配，swift会在返回表达式的值之前把表达式值的类型转为调用者期望的类型

When a return statement is not followed by an expression, it can be used only to return from a function or method that does not return a value (that is, when the return type of the function or method is Void or ()).

> return-statement -> return [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)opt

而当只写return时，仅仅是将控制权从该函数或方法传递给调用者，而不返回一个值。（这就是说，该函数或方法的返回类型为Void或()）

> return-statement -> return [expression](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html#//apple_ref/swift/grammar/expression)opt
