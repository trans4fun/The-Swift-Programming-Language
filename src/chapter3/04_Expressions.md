# Expressions
# 表达式

In Swift, there are four kinds of expressions: prefix expressions, binary expressions, primary expressions, and postfix expressions. Evaluating an expression returns a value, causes a side effect, or both.

在swift中有四种表达式：前缀表达式，二元表达式，主表达式和后缀表达式。对表达式求值可以得到一个返回值、或完成某些逻辑运算，或同时完成这两件事。

Prefix and binary expressions let you apply operators to smaller expressions. Primary expressions are conceptually the simplest kind of expression, and they provide a way to access values. Postfix expressions, like prefix and binary expressions, let you build up more complex expressions using postfixes such as function calls and member access. Each kind of expression is described in detail in the sections below.

前缀和二元表达式可以让我们在更短小的表达式中运算符。主表达式从概念上来看是最简单短小的表达式，同时又提供了一种求值的途径。后缀表达式，与前缀表达式和二元表达式相似，都可以让你建立更为复杂的表达方式，比如函数调用和成员访问。我们将在本节中详细解释每种表达式。

> GRAMMAR OF AN EXPRESSION

> expression → prefix-expressionbinary-expressionsopt

> expression-list → expression  expression,expression-list


## Prefix Expressions
## 前缀表达式

Prefix expressions combine an optional prefix operator with an expression. Prefix operators take one argument, the expression that follows them.

前缀表达式由一个任意前缀运算符接表达式构成。前缀表达式只接受一个参数。

The Swift standard library provides the following prefix operators:

* ++ Increment
* -- Decrement
* ! Logical NOT
* ~ Bitwise NOT
* \+ Unary plus
* \- Unary minus


Swift标准库提供了如下前缀运算符：

* ++ 自增
* -- 自减
* ! 逻辑否
* ~ 按位否
* \+ 一元加
* \- 一元负


For information about the behavior of these operators, see Basic Operators and Advanced Operators.

关于这些运算符的信息，请参见：“Basic Operators and Advanced Operators.”两节。


In addition to the standard library operators listed above, you use & immediately before the name of a variable that’s being passed as an in-out argument to a function call expression. For more information and to see an example, see In-Out Parameters.


作为对上述运算符的补充，你可以在作为某个函数参数的变量名前使用‘&’运算符。更多信息和实例，参见：In-Out Parameters一节。

> “GRAMMAR OF A PREFIX EXPRESSION

> 前缀表达式语法

> prefix-expression → prefix-operatoroptpostfix-expression

> prefix-expression → in-out-expression
‌ in-out-expression → &identifier
 

## Binary Expressions

## 二元表达式


Binary expressions combine an infix binary operator with the expression that it takes as its left-hand and right-hand arguments. It has the following form:

二元表达式由中缀二元运算符和“左边参数”与“右边参数”组成。形式如下：

       left-hand argument  operator  right-hand argument


The Swift standard library provides the following binary operators:

Swift标准库提供了如下的二元运算符：


* Exponentiative (No associativity, precedence level 160)
    * << Bitwise left shift
    * \>> Bitwise right shift

* 指数（无结合性，优先级160）
    * << 按位左移
    * \>> 按位右移
    
    
* Multiplicative (Left associative, precedence level 150)
    * Multiply
    * / Divide
    * % Remainder
    * &* Multiply, ignoring overflow
    * &/ Divide, ignoring overflow
    * &% Remainder, ignoring overflow
    * & Bitwise AND

* 乘法（左结合，优先级150）
	* \* 乘
	* / 除
	* % 求余
	* &* 乘，ignoring overflow
	* &/ 除，ignoring overflow
	* &% 求余，ignoring overflow
	* & 按位与


* Additive (Left associative, precedence level 140)
	* \+ Add
	* \- Subtract
	* &+ Add with overflow
	* &- Subtract with overflow
	* | Bitwise OR
	* ^ Bitwise XOR

* 加法（左结合，优先级140）
	* \+ 加 
	* \- 减
	* &+ 加，with overflow
	* &- 减，with overflow
	* | 按位或
	* ^ 按位异或
	
* Range (No associativity, precedence level 135)
	* .. Half-closed range
	* ... Closed range

* 值域（无结合性，优先级135）
	* .. 半闭值域
	* ... 闭值域
	
* Cast (No associativity, precedence level 132)
	* is Type check
	* as Type cast

* 类型转换（无结合性，优先级132）
	* is 类型检查
	* as 类型转换
	
* Comparative (No associativity, precedence level 130)
	* < Less than
	* <= Less than or equal
	* \> Greater than
	* \>= Greater than or equal
	* == Equal
	* != Not equal
	* === Identical
	* !== Not identical
	* ~= Pattern match

* 比较（无结合性，优先级130）
	* < 小于
	* <= 小于等于
	* \> 大于
	* \>= 大于等于
	* == 等于
	* != 不等于
	* === 恒等于
	* !== 不恒等
	* ~= 模式匹配

* Conjunctive (Left associative, precedence level 120)
	* && Logical AND

* 合取性(conjunctive)（左结合，优先级120）
	* && 逻辑与 

* Disjunctive (Left associative, precedence level 110)
	* || Logical OR

* 析取性(disjunction)（左结合，优先级110）
	* || 逻辑或
	

* Ternary Conditional (Right associative, precedence level 100)
	* ?: Ternary conditional

* 三元条件（右结合，优先级100）
	* ?: 三元条件

* Assignment (Right associative, precedence level 90)
	* = Assign
	* *= Multiply and assign
	* /= Divide and assign
	* %= Remainder and assign
	* += Add and assign
	* -= Subtract and assign
	* <<= Left bit shift and assign
	* \>>= Right bit shift and assign
	* &= Bitwise AND and assign
	* ^= Bitwise XOR and assign
	* |= Bitwise OR and assign
	* &&= Logical AND and assign
	* ||= Logical OR and assign


* 赋值（右结合，优先级90）
	* = 赋值
	* *= 乘等
	* /= 除等
	* %= 余等
	* += 加等
	* -= 减等
	* <<= 左移等
	* \>>= 右移等
	* &= 按位与等
	* ^= 按位异或等
	* |= 按位非等
	* &&= 逻辑与等
	* ||= 逻辑或等

For information about the behavior of these operators, see Basic Operators and Advanced Operators.


关于这些运算符的信息，请参见：Basic Operators and Advanced Operators两节。

> NOTE
> 注解

> At parse time, an expression made up of binary operators is represented as a flat list. This list is transformed into a tree by applying operator precedence For example, the expression 2 + 3 * 5 is initially understood as a flat list of five items, 2, +, `` 3``, *, and 5. This process transforms it into the tree (2 + (3 * 5)).

> 在解析时，由二元操作符构成的表达式被表达为一个简单列表。这个列表按照运算符的优先级被转换成树（tree），比如“2 + 3 * 5”首先被认为是'2'、'+'、'3'、'+'、'5'这5个元素，随后被转换成树(2 + (3 * 5))。



> 二元表达式语法

> GRAMMAR OF A BINARY EXPRESSION

‌> binary-expression → binary-operatorprefix-expression

‌> binary-expression → assignment-operatorprefix-expression

‌> binary-expression → conditional-operatorprefix-expression

‌> binary-expression → type-casting-operator

‌> binary-expressions → binary-expressionbinary-expressionsopt


## Assignment Operator
## 赋值运算符

The assigment operator sets a new value for a given expression.It has the following form:

赋值运算符会给某个给定的表达式赋值。如下面的例子：

    expression = value

The value of the expression is set to the value obtained by evaluating the value. If the expression is a tuple, the value must be a tuple with the same number of elements. (Nested tuples are allowed.) Assignment is performed from each part of the value to the corresponding part of the expression. For example:


上面语句的意思就是计算`value`的值并赋给`expression`。如果`expression`是个元组，那么`value`必须是含有同等数量元素的元祖。（嵌套元祖也是可以直接赋值滴。）元祖赋值会把`value`中相对应的部分分别赋给`expression`。例如：

    > (a, _, (b, c)) = ("test", 9.45, (12, 3))

    > // a is "test", b is 12, c is 3, and 9.45 is ignored


The assignment operator does not return any value.

赋值运算符不返回任何值。

> GRAMMAR OF AN ASSIGNMENT OPERATOR

> 赋值运算符的语法

> assignment-operator → =


## Ternary Conditional Operator

## 三元条件运算符

The ternary conditional operator evaluates to one of two given values based on the value of a condition. It has the following form:


三元条件运算符是根据一个条件判断来求值。形式如下：

    condition ? expression used if true : expression used if false


If the condition evaluates to true, the conditional operator evaluates the first expression and returns its value. Otherwise, it evaluates the second expression and returns its value. The unused expression is not evaluated.

上面例子中，当condition的值为true时，那么将对第一个表达式求值并返回。否则将对第二个表达式求值并返回。期间没有用到的那个表达式将不会被调用。

For an example that uses the ternary conditional operator, see Ternary Conditional Operator.

更多三元条件运算符的例子，请参见Ternary Conditional Operator。

> GRAMMAR OF A CONDITIONAL OPERATOR

> 条件运算符语法：

> conditional-operator → ?expression:


## Type-Casting Operators
## 类型转换运算符

There are two type-casting operators, the as operator and the is operator. They have the following form:

类型转换运算符有两种：as运算符合is运算符。形式如下：


    expression as type

    expression as? type

    expression is type


The as operator performs a cast of the expression to the specified type. It behaves as follows:

上面例子中，as 运算符会把目标表达式`expression`转换成指定的类型`type`。过程如下：

* If conversion to the specified type is guaranteed to succeed, the value of the expression is returned as an instance of the specified type. An example is casting from a subclass to a superclass.

* 如果转换为`type`类型保证能够成功，那么目标表达式`expression`就会返回指定类型的实例。一个显而易见的例子就是子类类型转换成父类类型。

* If conversion to the specified type is guaranteed to fail, a compile-time error is raised.

* 如果转换失败，则抛出编译错误。

* Otherwise, if it’s not known at compile time whether the conversion will succeed, the type of the cast expresion is an optional of the specified type. At runtime, if the cast succeeds, the value of expression is wrapped in an optional and returned; otherwise, the value returned is nil. An example is casting from a superclass to a subclass.

* 如果不是以上两种情况，那么目标表达式`expression`就会被转换成指定类型的optional。在运行时，如果转换成功，那么`expression`会返回一个optional的包装类型；否则返回nil。举个例子：

> class SomeSuperType {}

> class SomeType: SomeSuperType {}

> class SomeChildType: SomeType {}

> let s = SomeType()

> let x = s as SomeSuperType  // known to succeed; type is SomeSuperType

> let y = s as Int            // known to fail; compile-time error

> let z = s as SomeChildType  // might fail at runtime; type is SomeChildType?


Specifying a type with as provides the same information to the compiler as a type annotation, as shown in the following example:

使用as指定类型与使用类型注释效果相同，看下面这个例子：

> let y1 = x as SomeType  // Type information from 'as'

> let y2: SomeType = x    // Type information from an annotation


The is operator checks at runtime to see whether the expression is of the specified type. If so, it returns true; otherwise, it returns false.


is运算符会在运行时检查`expression`是否指定了类型。成功会返回true, 否则 false。上述检查在编译时不可用，下面例子就是无效的：

> "hello" is String
> 
  "hello" is Int


For more information about type casting and to see more examples that use the type-casting operators, see Type Casting.

关于类型转换的更多内容和例子，请参见： Type Casting.

> GRAMMAR OF A TYPE-CASTING OPERATOR

> 类型转换的语法

> type-casting-operator → is­ type­| as­?(opt)­ type


## Primary Expressions
## 主表达式

Primary expressions are the most basic kind of expression. They can be used as expressions on their own, and they can be combined with other tokens to make prefix expressions, binary expressions, and postfix expressions.

主表达式是种最基本的表达式。它可以单独使用，也可以和其他表达式组合使用。

> GRAMMAR OF A PRIMARY EXPRESSION

> 主表达式的语法

> primary-expression → identifiergeneric-argument-clauseopt
> primary-expression → literal-expression
> primary-expression → self-expression
> primary-expression → superclass-expression
> primary-expression → closure-expression
> primary-expression → parenthesized-expression
> primary-expression → implicit-member-expression
> primary-expression → wildcard-expression


## Literal Expression
## 字面量表达式

A literal expression consists of either an ordinary literal (such as a string or a number), an array or dictionary literal, or one of the following special literals:

一个字面量表达式可以由普通文本（比如一个字符串或者一个数字）、一个数组或字典字面量或以下指定的文本组成：


Literal      | Type    | Value
------------ | --------| ------------
\__FILE__    | String  | The name of the file in which it appears.
\__LINE__    | Int     | The line number on which it appears.
\__COLUMN__  | Int     | The column number in which it begins.
\__FUNCTION__| String  | The name of the declaration in which it appears.

Literal      | Type    | Value
------------ | --------| ------------
\__FILE__    | String  | 当前文件的文件名
\__LINE__    | Int     | 当前行数
\__COLUMN__  | Int     | 当前列数
\__FUNCTION__| String  | 当前声明的名字


Inside a function, the value of __FUNCTION__ is the name of that function, inside a method it is the name of that method, inside a property getter or setter it is the name of that property, inside special members like init or subscript it is the name of that keyword, and at the top level of a file it is the name of the current module.


在函数中，__FUNCTION__的值为当前函数的名字。在方法中，它的值为当前方法的名字。在某个属性的getter/setter中为这个属性的名字。在像init和subscript这样的特殊成员中，它的值为那个关键字的名字。在文件顶层（at the top level of a file）则是当前模块的名字。


An array literal is an ordered collection of values. It has the following form:


数组字面量是有序的值的集合。形式如下：

     [value 1, value 2, ...]


The last expression in the array can be followed by an optional comma. An empty array literal is written as an empty pair of brackets ([]). The value of an array literal has type T[], where T is the type of the expressions inside it. If there are expressions of multiple types, T is their closest common supertype.

数组中的最后一个表达式后面可以接一个逗号。一对空的中括号（[]）组成了一个空的数组字面量。数组字面量的类型是T[]，这个T就是数组中表达式的类型。如果数组含多个类型的表达式，T则是他们的最近公共父类型（closest common supertype）。

A dictionary literal is an unordered collection of key-value pairs. It has the following form: 

字典字面量是无序键值对的集合。形式如下：

    [key 1: value 1, key 2: value 2, ...]


The last expression in the dictionary can be followed by an optional comma. An empty dictionary literal is written as a colon inside a pair of brackets ([:]) to distinguish it from an empty array literal. The value of a dictionary literal has type Dictionary<KeyType, ValueType>, where KeyType is the type of its key expressions and ValueType is the type of its value expressions. If there are expressions of multiple types, KeyType and ValueType are the closest common supertype for their respective values.


字典中的最后一个表达式后面也可以接一个逗号。一对空的中括号包含一个冒号（[:]）组成了一个空的字典字面量。字典字面量的类型是Dictionary<KeyType, ValueType>，这里KeyType、ValueType就是key和value的类型。如果包含多个类型，则分别取他们相应的最近的公共父类型（closest common supertype）。

> GRAMMAR OF A LITERAL EXPRESSION

> 字面量表达式的语法

> literal-expression → literal

> literal-expression → array-literal | dictionary-literal

> literal-expression → __FILE__ | __LINE__  __COLUMN__ | __FUNCTION__

> array-literal → [array-literal-itemsopt]

> array-literal-items → array-literal-item,opt | array-literal-item,array-literal-items

> array-literal-item → expression

> dictionary-literal → [dictionary-literal-items] | [:] | dictionary-literal-items → dictionary-literal-item,opt dictionary-literal-item,dictionary-literal-items

> dictionary-literal-item → expression:expression


## Self Expression
## self表达式


The self expression is an explicit reference to the current type or instance of the type in which it occurs. It has the following forms:

self表达式是对当前类型或当前实例的直接引用。形式如下：

    self
 
    self.member name
    
    self[subscript index]
    
    self(initializer arguments)
     
     self.init(initializer arguments)


In an initializer, subscript, or instance method, self refers to the current instance of the type in which it occurs. In a static or class method, self refers to the current type in which it occurs.


如果在初始设定式、子脚本、实例方法中，self为当前类型实例的引用。在静态方法和类方法中，self为当前类型的引用。


The self expression is used to specify scope when accessing members, providing disambiguation when there is another variable of the same name in scope, such as a function parameter. For example:

self表达式被用于在访问成员变量时指定作用域，当作用域中有重名变量时，它还用来消除歧义（例如函数的参数）。例如：

    class SomeClass {
        var greeting: String
        init(greeting: String) {
            self.greeting = greeting
        }
    }


In a mutating method of value type, you can assign a new instance of that value type to self. For example:


在派生方法中，你可以把一个那个类型的新实例赋值给self。例如：

    struct Point {
        var x = 0.0, y = 0.0
        mutating func moveByX(deltaX: Double, y deltaY: Double) {
            self = Point(x: x + deltaX, y: y + deltaY)
        }
    }


> GRAMMAR OF A SELF EXPRESSION

> self表达式的语法

> self-expression → self

> self-expression → self.identifier

> self-expression → self[expression]

> self-expression → self.init


## Superclass Expression
## 超类表达式


A superclass expression lets a class interact with its superclass. It has one of the following forms:


超类表达式可以让我们在某个class中访问它的超类，形式如下：

    super.`member name`

    super[`subscript index`]

    super.init（`initializer arguments`）


The first form is used to access a member of the superclass. The second form is used to access the superclass’s subscript implementation. The third form is used to access an initializer of the superclass.

第一种形式用来访问超类的某个成员。第二种形式用来访问超类的子脚本实现（subscript implementation）。第三种用来访问该超类的初始设定式。


Subclasses can use a superclass expression in their implementation of members, subscripting, and initializers to make use of the implementation in their superclass.


子类可以利用超类的实现，并通过使用超类表达式来实现它们的成员、子脚本和初始值。

> GRAMMAR OF A SUPERCLASS EXPRESSION

> 超类表达式的语法

> superclass-expression → superclass-method-expression | superclass-subscript-expression  | superclass-initializer-expression

> superclass-method-expression → super.identifier

> superclass-subscript-expression → super[expression]

> superclass-initializer-expression → super.init


## Closure Expression
## 闭包表达式

A closure expression creates a closure, also known as a lambda or an anonymous function in other programming languages. Like function declarations, closures contain statements which they execute, and they capture values from their enclosing scope. It has the following form:

闭包表达式可以创建一个闭包，就好像其他语言中的lambda或者匿名函数。与函数声明相同，闭包包含了要执行的语句，接收作用域中的变量。形式如下：

    { (parameters) -> return type in
        statements
    }

The parameters have the same form as the parameters in a function declaration, as described in Function Declaration.

闭包的参数声明跟函数的参数一样，具体参见Function Declaration。

There are several special forms that allow closures to be written more concisely:


为了写起来更加简洁，闭包还有几种特殊形式：

* A closure can omit the types of its parameters, its return type, or both. If you omit the parameter names and both types, omit the in keyword before the statements. If the omitted types can’t be inferred, a compile-time error is raised.


* 闭包可以省略参数和返回值的类型。如果省略了参数和参数类型，语句前面的in也要省略。如果省略的类型不能被自动甄别，那么就会抛出编译错误。

* A closure may omit names for its parameters. Its parameters are then implicitly named $ followed by their position: $0, $1, $2, and so on.

* 闭包可以省略参数名。如果省略了它们则会隐式地命名为“$+它们的顺序号”：`$0`,`$1`,`$2`等。

* A closure that consists of only a single expression is understood to return the value of that expression. The contents of this expression is also considered when performing type inference on the surrounding expression.

* 如果闭包中只包含一个表达式，那么该表达式就会自动成为该闭包的返回值。同时表达式的内容在进行类型推断的时候也会参考周围的表达式。

The following closure expressions are equivalent:

以下几个表达式是等价的：

    myFunction {
        (x: Int, y: Int) -> Int in
        return x + y
    }
 
    myFunction {
        (x, y) in
        return x + y
    }
 
    myFunction { return $0 + $1 }
 
    myFunction { $0 + $1 }

For information about passing a closure as an argument to a function, see Function Call Expression.

关于将闭包作为函数参数的更多内容，请参见：Function Call Expression。

A closure expression can explicitly specify the values that it captures from the surrounding scope using a capture list. A capture list is written as a comma separated list surrounded by square brackets, before the list of parameters. If you use a capture list, you must also use the in keyword, even if you omit the parameter names, parameter types, and return type.

可以通过使用捕获列表从周围作用域中捕获值来显式指定给闭包表达式。捕获列表是以在参数列表前使用中括号加逗号分隔的形式组成的。一旦使用了参数列表，即使省略了参数名，参数类型和返回值类型，也要使用in关键字。

Each entry in the capture list can be marked as weak or unowned to capture a weak or unowned reference to the value.

捕获列表中的每一项都要标记为weak或unowned来捕获弱引用和无主引用。

    myFunction{ print（self.title） }                            
         // strong capture
    myFunction { [weak self] in     print（self!.title） }    
        // weak capture
    myFunction { [unowned self] in print（self.title） }  
        // unowned capture

在捕获列表中，你能绑定任意表达式给一个命名值。表达式在闭包形成时被根据指定强度计算并捕获。

    // Weak capture of "self.parent" as "parent"
    myFunction { [weak parent = self.parent] in print(parent!.title) }

For more information and examples of closure expressions, see Closure Expressions.

关于闭包表达式更多信息和例子，请参见 Closure Expressions。

> GRAMMAR OF A CLOSURE EXPRESSION

> 闭包表达式的语法

> closure-expression → {closure-signatureoptstatements}
> 
> closure-signature → parameter-clausefunction-resultoptin
> 
> closure-signature → identifier-listfunction-resultoptin
> 
> closure-signature → capture-listparameter-clausefunction-resultoptin
> 
> closure-signature → capture-listidentifier-listfunction-resultoptin
> 
> closure-signature → capture-listin
> 
> capture-list → [capture-specifierexpression]
> 
> capture-specifier → weak | unowned | unowned(safe)| unowned(unsafe)


# Implicit Member Expression
# 隐式成员表达式

An implicit member expression is an abbreviated way to access a member of a type, such as an enumeration case or a class method, in a context where type inference can determine the implied type. It has the following form:


在可以判断隐藏类型的上下文中，隐式成员表达式是访问某个类型的成员的简便写法，例如在枚举或类方法中。形式如下：

    .member name

For example:

例子：

    var x = MyEnumeration.SomeValue
    x = .AnotherValue

> GRAMMAR OF A IMPLICIT MEMBER EXPRESSION

> 隐式成员表达式的语法：

> implicit-member-expression → .identifier


## Parenthesized Expression
## 圆括号表达式

A parenthesized expression consists of a comma-separated list of expressions surrounded by parentheses. Each expression can have an optional identifier before it, separated by a colon (:). It has the following form:

 
圆括号表达式由中括号包裹的一组逗号分隔的子表达式列表组成。每个子表达式前面可以有一个可选标识符，由`:`隔开。形式如下：

    （identifier 1: expression 1, identifier 2: expression 2, ...）

Use parenthesized expressions to create tuples and to pass arguments to a function call. If there is only one value inside the parenthesized expression, the type of the parenthesized expression is the type of that value. For example, the type of the parenthesized expression (1) is Int, not (Int).


圆括号表达式可以用来创建元祖或给函数传参。如果圆括号表达式中只有一个值，那么这个表达式的类型则与此值相同，例如表达式`(1)`的类型为`Int`而不是`(Int)`。

> GRAMMAR OF A PARENTHESIZED EXPRESSION

> 圆括号表达式的语法

> parenthesized-expression → (expression-element-listopt)
> 
> expression-element-list → expression-element  expression-element,expression-element-list
> 
> expression-element → expression  identifier:expression


## Wildcard Expression
## 通配符表达式

A wildcard expression is used to explicitly ignore a value during an assignment. For example, in the following assignment 10 is assigned to x and 20 is ignored:

通配符表达式用来在赋值的时候显式地忽略某个值。比如下面的赋值语句中，`10`被传递给`x`，`20`则被忽略。

     (x, _) = (10, 20)
     // x is 10, 20 is ignored


> GRAMMAR OF A WILDCARD EXPRESSIO

> 通配符表达式的语法

> wildcard-expression → _


## Postfix Expressions
## 后缀表达式

Postfix expressions are formed by applying a postfix operator or other postfix syntax to an expression. Syntactically, every primary expression is also a postfix expression.


后缀表达式由一个表达式后面加上一个后缀操作符或其他后缀语法组成。单纯从语法上讲，每个主表达式也是一个后缀表达式。

The Swift standard library provides the following postfix operators:

* ++ Increment
* -- Decrement

swift标准库提供了如下后缀操作符：
 
* ++ 自增
* -- 自减

For information about the behavior of these operators, see Basic Operators and Advanced Operators.

关于这些表达式行为的更多信息，请参见“Basic Operators and Advanced Operators.”

> GRAMMAR OF A POSTFIX EXPRESSION

> 后缀表达式的语法
> 
> postfix-expression → primary-expression
> 
> postfix-expression → postfix-expressionpostfix-operator
> 
> postfix-expression → function-call-expression
> 
> postfix-expression → initializer-expression
> 
> postfix-expression → explicit-member-expression
> 
> postfix-expression → postfix-self-expression
> 
> postfix-expression → dynamic-type-expression
> 
> postfix-expression → subscript-expression
> 
> postfix-expression → forced-value-expression
> 
> postfix-expression → optional-chaining-expression


## Function Call Expression
## 函数调用表达式

A function call expression consists of a function name followed by a comma-separated list of the function’s arguments in parentheses. Function call expressions have the following form:


函数调用表达式由函数名后加圆括号组成，圆括号里面为逗号分隔的函数参数列表。形式如下：

     function name(argument value 1, argument value 2)

The function name can be any expression whose value is of a function type.

上面的`function name`可以是任何返回值为函数类型的表达式。

If the function definition includes names for its parameters, the function call must include names before its argument values separated by a colon (:). This kind of function call expression has the following form:

如果函数声明中包含了参数名，那么函数调用时必须在参数值前加上参数名，并用分号隔开。这种函数调用表达式形式如下：

    function name(argument name 1: argument value 1, argument name 2: argument value 2)

A function call expression can include a trailing closure in the form of a closure expression immediately after the closing parenthesis. The trailing closure is understood as an argument to the function, added after the last parenthesized argument. The following function calls are equivalent:

函数调用表达式可以包含一个由紧跟在圆括号后面由一个闭包表达式组成的尾随闭包（`trailing closure`）。追加在圆括号后面的尾随闭包会被当做函数的参数。下面两种写法均可：

     // someFunction takes an integer and a closure as its arguments
     
    someFunction(x, {$0 == 13})
    
    someFunction(x) {$0 == 13}

If the trailing closure is the function’s only argument, the parentheses can be omitted.

如果这个闭包是函数的唯一参数，那么圆括号可以省略。

     // someFunction takes a closure as its only argument
     
    myData.someMethod() {$0 == 13}
    
    myData.someMethod {$0 == 13}

> GRAMMAR OF A FUNCTION CALL EXPRESSION

> 函数调用表达式语法

> function-call-expression → postfix-expressionparenthesized-expression

> function-call-expression → postfix-expressionparenthesized-expressionopttrailing-closure
> 
> trailing-closure → closure-expression


## Initializer Expression

## 初始化函数表达式

An initializer expression provides access to a type’s initializer. It has the following form:

初始化函数表达式用来给类型初始化。形式如下：

     expression.init（initializer arguments）


You use the initializer expression in a function call expression to initialize a new instance of a type. Unlike functions, an initializer can’t be used as a value. For example:

你可以在函数调用表达式中使用初始化函数表达式来初始化一个类型的实例。初始化函数不像函数，它不能有返回值，例如：

    var x = SomeClass.someClassFunction // ok

    var y = SomeClass.init              // error

You also use an initializer expression to delegate to the initializer of a superclass.

初始化函数表达式还可以用来完成对父类初始化函数的代理。

    class SomeSubClass: SomeSuperClass {
        init() {
            // subclass initialization goes here
            super.init()
        }
    }

> GRAMMAR OF AN INITIALIZER EXPRESSION

> 初始化函数表达式的语法

> initializer-expression → postfix-expression.init


## Explicit Member Expression
## 显式成员表达式

A explicit member expression allows access to the members of a named type, a tuple, or a module. It consists of a period (.) between the item and the identifier of its member.

显示成员表达式允许我们访问已命名类型、元祖或模块的成员。它由元素和成员的标识符以及二者之间的点（`.`）组成。

    expression.member name

The members of a named type are named as part of the type’s declaration or extension. For example:

对于已命名类型，成员是类型定义或扩展的一部分。例如：

    class SomeClass {
        var someProperty = 42
    }
    let c = SomeClass()
    let y = c.someProperty  // Member access

The members of a tuple are implicitly named using integers in the order they appear, starting from zero. For example:

对于元祖，成员通过从零开始的它们出现的顺序整数来访问。例如：

    var t = (10, 20, 30)
    t.0 = t.1
    // Now t is (20, 20, 30)

The members of a module access the top-level declarations of that module.

对于模块，成员访问的是模块的顶级（top-level）声明。

> GRAMMAR OF AN EXPLICIT MEMBER EXPRESSION

> 显示成员表达式的语法

> explicit-member-expression → postfix-expression.decimal-digit
> 
> explicit-member-expression → postfix-expression.identifiergeneric-argument-clauseopt


## Postfix Self Expression
## 后缀self表达式

A postfix self expression consists of an expression or the name of a type, immediately followed by .self. It has the following forms:

后缀self表达式由表达式或类名接一个`.self`组成。形式如下：

    expression.self
    type.self

The first form evaluates to the value of the expression. For example, x.self evaluates to x.

第一种形式计算出表达式（`expression`）的值。例如`x.self`就等于`x`。

The second form evaluates to the value of the type. Use this form to access a type as a value. For example, because SomeClass.self evaluates to the SomeClass type itself, you can pass it to a function or method that accepts a type-level argument.

第二种形式计算出对应类型（`type`）的值。这种形式可以将某类型作为一个值来访问。例如，由于`SomeClass.self`等于`SomeClass`本身，所以你可以将其传给一个函数或方法。

> GRAMMAR OF A SELF EXPRESSION

> 后缀self表达式的语法

> postfix-self-expression → postfix-expression.self



## Dynamic Type Expression
## 动态类型表达式

A dynamicType expression consists of an expression, immediately followed by .dynamicType. It has the following form:


动态类型（`dynamicType`）表达式由表达式接`.dynamicType`组成。形式如下：

    expression.dynamicType

The expression can’t be the name of a type. The entire dynamicType expression evaluates to the value of the runtime type of the expression, as the following example shows:

表达式不能是类型的名字。整个动态类型表达式计算出表达式运行时的值，参见下例：

    class SomeBaseClass {
        class func printClassName() {
            println("SomeBaseClass")
        }
    }
    class SomeSubClass: SomeBaseClass {
        override class func printClassName() {
            println("SomeSubClass")
        }
    }
    let someInstance: SomeBaseClass = SomeSubClass()
    // someInstance is of type SomeBaseClass at compile time, but
    // someInstance is of type SomeSubClass at runtime
    someInstance.dynamicType.printClassName()
    // prints "SomeSubClass

> GRAMMAR OF A DYNAMIC TYPE EXPRESSION

> 动态类型表达式的语法

> dynamic-type-expression → postfix-expression.dynamicType


## Subscript Expression
## 下标表达式

A subscript expression provides subscript access using the getter and setter of the corresponding subscript declaration. It has the following form:

下标表达式提供了通过响应的下标声明来访问getter/setter方法。形式如下：

    expression[index expressions]
    
To evaluate the value of a subscript expression, the subscript getter for the expression’s type is called with the index expressions passed as the subscript parameters. To set its value, the subscript setter is called in the same way.

下标表达式可以通过传递下标参数（`index expressions`）计算getter的值，setter亦同理。

For information about subscript declarations, see Protocol Subscript Declaration.

更多关于下标声明的信息，参见Protocol Subscript Declaration。

> GRAMMAR OF A SUBSCRIPT EXPRESSION

> 下标表达式语法：
> 
> subscript-expression → postfix-expression[expression-list]


## Forced-Value Expression
## 强取值表达式

A forced-value expression unwraps an optional value that you are certain is not nil. It has the following form:

强取值表达式用于对非空（not `nil`）的可选值进行拆包。形式如下：

     expression!

If the value of the expression is not nil, the optional value is unwrapped and returned with the corresponding nonoptional type. Otherwise, a runtime error is raised.

上式中，如果一个`expression`的值不是`nil`，那么该可选值会被拆包并返回响应的类型。否则抛出运行时错误。

> GRAMMAR OF A FORCED-VALUE EXPRESSION
> 
> 强取值表达式的语法：
> 
> forced-value-expression → postfix-expression!


## Optional-Chaining Expression
## 可选链式表达式

An optional-chaining expression provides a simplified syntax for using optional values in postfix expressions. It has the following form:

可选链式表达式提供一种在后缀表达式中使用可选值的简化的语法。形式如下：

    expression?

On its own, the postfix ? operator simply returns the value of its argument as an optional.

后缀`?`表达式就是简单的将所传参数作为可选值返回。

Postfix expressions that contain an optional-chaining expression are evaluated in a special way. If the optional-chaining expression is nil, all of the other operations in the postfix expression are ignored and the entire postfix expression evaluates to nil. If the optional-chaining expression is not nil, the value of the optional-chaining expression is unwrapped and used to evaluate the rest of the postfix expression. In either case, the value of the postfix expression is still of an optional type.

包含可选链式表达式的后缀表达式计算起来比较特殊。如果可选链式表达式为`nil`，所有在此后缀表达式中的操作符都将被忽略，然后整个后缀表达式返回`nil`。如果不为`nil`，则可选链式表达式被拆包然后应用于后续的计算。在这两种情况下，该后缀表达式仍然是一个可选值。

If a postfix expression that contains an optional-chaining expression is nested inside other postfix expressions, only the outermost expression returns an optional type. In the example below, when c is not nil, its value is unwrapped and used to evaluate both .property and .performAction(), and the entire expression c?.property.performAction() has a value of an optional type.

如果一个包含可选链式表达式的后缀表达式嵌套在其他后缀表达式中，只有最外层的返回一个可选类型。下面例子中，当`c`不为`nil`，时，它将被拆包然后用于`.property`和`.performAction()`的计算，整个表达式`c?.property.performAction() `拥有一个可选类型的值。

    var c: SomeClass?
    var result: Bool? = c?.property.performAction()

The following example shows the behavior of the example above without using optional chaining.

如果不使用可选链表达式，那么上面例子的代码等价于：

    if let unwrappedC = c {
        result = unwrappedC.property.performAction（）
    }

> GRAMMAR OF AN OPTIONAL-CHAINING EXPRESSION
> 
> 可选链式表达式的语法

> optional-chaining-expression → postfix-expression?

