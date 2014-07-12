
# 表达式

在swift中有四种表达式：前缀表达式，二元表达式，主表达式和后缀表达式。对表达式求值可以得到一个返回值、或完成某些逻辑运算，或同时完成这两件事。

前缀和二元表达式可以让你在更短小的表达式中使用运算符。主表达式从概念上来看是最简单的表达式，并提供了一种求值的方式。后缀表达式，与前缀表达式和二元表达式相似，都可以让你建立更为复杂的表达方式，比如函数调用和成员访问。我们将在本节中详细解释每种表达式。

> 表达式语法

> 表达式 → 前置表达式 二元表达式列表 可选

> 表达式列表 → 表达式 | 表达式 **,** 表达式列表


## 前缀表达式

前缀表达式由一个任意前缀运算符和表达式构成。前缀表达式只接受一个参数。

Swift标准库提供了如下前缀运算符：

* ++ 自增
* -- 自减
* ! 逻辑否
* ~ 按位否
* \+ 一元加
* \- 一元负


关于这些运算符的信息，请参见：“Basic Operators and Advanced Operators.”。


除了上面标准库的运算符列表，你可以在调用函数的参数变量名前使用‘&’。？？
除了上述标准库运算符外，你可以在作为某个函数参数的变量名前使用‘&’运算符。更多信息和例子，请见：In-Out Parameters。

> 前缀表达式语法

> 前置表达式 → 前置运算符 可选 后置表达式

> 前置表达式 → 写入写出表达式
> 写入写出表达式 → **&** 标识符
 


## 二元表达式

二元表达式由‘左边表参数’＋‘中缀二元操作符’＋‘右边参数’组成。形式如下：

       left-hand argument  operator  right-hand argument

Swift标准库提供了以下的二元运算符：

* 指数（无结合性，优先级160）
    * << 按位左移
    * \>> 按位右移

* 乘法（左结合，优先级150）
	* \* 乘
	* / 除
	* % 求余
	* &* 乘，ignoring overflow
	* &/ 除，ignoring overflow
	* &% 求余，ignoring overflow
	* & 按位与

* 加法（左结合，优先级140）
	* \+ 加 
	* \- 减
	* &+ 加，with overflow
	* &- 减，with overflow
	* | 按位或
	* ^ 按位异或

* 值域（无结合性，优先级135）
	* .. 半闭值域
	* ... 闭值域
	

* 类型转换（无结合性，优先级132）
	* is 类型检查
	* as 类型转换

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

* 合取性(conjunctive)（左结合，优先级120）
	* && 逻辑与 

* 析取性(disjunction)（左结合，优先级110）
	* || 逻辑或

* 三元条件（右结合，优先级100）
	* ?: 三元条件

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

关于这些运算符的使用信息，请参见：Basic Operators and Advanced Operators。

> 注解

> 在解析时，由二元操作符构成的表达式被视为一个简单列表。这个列表按照运算符的优先级被转换成树（tree），比如“2 + 3 * 5”首先被理解为一个5个元素的列表：'2'、'+'、'3'、'+'、'5'，随后被转换成树(2 + (3 * 5))。



> 二元表达式语法

> 二元表达式 → 二元运算符 前置表达式

> 二元表达式 → 赋值运算符 前置表达式

> 二元表达式 → 条件运算符 前置表达式

> 二元表达式 → 类型转换运算符

> 二元表达式列表 → 二元表达式 二元表达式列表 可选


## 赋值运算符

赋值运算符会给某个给定的表达式赋值。形式如下：

    expression = value

表达式的意思就是计算`value`的值并赋给`expression`。如果`expression`是个元组，那么`value`必须是含有同等数量元素的元祖。（嵌套元祖亦可。）元祖赋值会把`value`中相对应的部分分别赋给`expression`。例如：

    > (a, _, (b, c)) = ("test", 9.45, (12, 3))

    > // a is "test", b is 12, c is 3, and 9.45 is ignored


赋值运算符不返回任何值。

> 赋值运算符的语法

> 赋值运算符 → **=**


## 三元条件运算符

三元条件运算符是根据一个条件判断来求值。形式如下：

    condition ? expression used if true : expression used if false

如果condition的值为true时，那么就对第一个表达式求值并返回。否则就对第二个表达式求值并返回。没有用到的表达式将不会被调用。

更多三元条件运算符的例子，请参见Ternary Conditional Operator。


> 条件运算符语法：

> 三元条件运算符 → **?** 表达式 **:**


## 类型转换运算符

类型转换运算符有两种：as运算符和is运算符。形式如下：


    expression as type

    expression as? type

    expression is type


as 运算符会把目标表达式`expression`转换成指定的类型`type`。方式如下：


* 如果能够保证成功转换为指定类型，那么目标表达式`expression`就会返回指定类型的实例。典型的例子就是子类转换为超类。

* 如果转换到指定类型肯定失败，则抛出编译错误。


如果在编译的时候不知道转换是否成功，那么转换表达式的类型是指定类型的可选类型。在运行时，如果转换成功，表达式会被包装成一个可选类型并返回。
否则，返回nil。对应的例子就是子类转换为超类：

> class SomeSuperType {}

> class SomeType: SomeSuperType {}

> class SomeChildType: SomeType {}

> let s = SomeType()

> let x = s as SomeSuperType  // known to succeed; type is SomeSuperType

> let y = s as Int            // known to fail; compile-time error

> let z = s as SomeChildType  // might fail at runtime; type is SomeChildType?


使用as指定类型与使用类型注释对编译器来说是一样的，看下面这个例子：

> let y1 = x as SomeType  // Type information from 'as'

> let y2: SomeType = x    // Type information from an annotation


is运算符会在运行时检查`expression`是否指定了类型。如果是，则返回true, 否则 返回false。

 
在编译时编译器不检查它们是true还是false，下面例子是无效的：

> "hello" is String
> 
  "hello" is Int


更多关于类型转换和使用类型转换操作符的例子，请参见： Type Casting.

> 类型转换的语法

> 类型转换运算符 → **is** 类型 | **as ?** 可选 类型


## 主表达式

主表达式是种最基础的表达式。它可以单独作为表达式使用，也可以和其他符号一起使用组合成前缀表达式、二元表达式和后缀表达式。

> 主表达式的语法

> 主表达式 → 标识符 泛型参数子句 可选
> 主表达式 → 字面量表达式
> 主表达式 → self表达式
> 主表达式 → 超类表达式
> 主表达式 → 闭包表达式
> 主表达式 → 圆括号表达式
> 主表达式 → 隐式成员表达式
> 主表达式 → 通配符表达式


## 字面量表达式

一个字面量表达式可以由普通文本（比如一个字符串或一个数字）、数组或字典字面量，或以下指定字面量组成：


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


在函数中，__FUNCTION__的值是当前函数的名字。在方法中，它的值是当前方法的名字。在内部getter/setter属性中，它就是属性的名字。在init和subscript这样特殊成员中，它的值是关键字的名字。在文件顶层（at the top level of a file），它是前模块的名字。


数组字面量是一个有序的值的集合。形式如下：

     [value 1, value 2, ...]


数组中的、最后一个表达式后面可以后跟一个逗号。一个空数组可以写成[].。数组字面量的类型是T[]，这个T就是数组中表达式的类型。如果数组含多个类型的表达式，T则是他们的最近公共超类型（closest common supertype）。


字典字面量是无序键值对的集合。形式如下：

    [key 1: value 1, key 2: value 2, ...]



字典中的最后一个表达式后面也可以跟一个逗号。 [:]组成了一个空的字典字面量。字典字面量的类型是Dictionary<KeyType, ValueType>，这里KeyType、ValueType就是key和value的类型。如果包含多个类型的表达式，KeyType 和ValueType分别取他们相应的最近的公共超类型（closest common supertype）。

> 字面量表达式的语法

> 字面量表达式 → 字面量

> 字面量表达式 → 数组字面量 | 字典字面量

> 字面量表达式 → \_\_FILE\_\_ | \_\_LINE\_\_ | \_\_COLUMN\_\_ | \_\_FUNCTION\_\_

> 数组字面量 → [ 数组字面量项列表 可选 ]

> 数组字面量项列表 → 数组字面量项 , 可选 | 数组字面量项 , 数组字面量项列表

> 数组字面量项 → 表达式
> 字典字面量 → [ 字典字面量项列表 ] | [ : ]
> 字典字面量项列表 → 字典字面量项 , 可选 | 字典字面量项 , 字典字面量项列表
> 字典字面量项 → 表达式 : 表达式
## self表达式


self表达式是对当前类型或当前实例的直接引用。形式如下：

    self
 
    self.member name
    
    self[subscript index]
    
    self(initializer arguments)
     
     self.init(initializer arguments)



如果在初始设定式、子脚本、实例方法中，self指向当前类型实例的引用。在静态方法和类方法中，self指向前类型的引用。


self表达式用于在访问成员变量时指定作用域，消除作用域中有重名变量的冲突，例如函数的参数。例如：

    class SomeClass {
        var greeting: String
        init(greeting: String) {
            self.greeting = greeting
        }
    }



在派生方法中，你可以把一个那个类型的新实例赋值给self。例如：

    struct Point {
        var x = 0.0, y = 0.0
        mutating func moveByX(deltaX: Double, y deltaY: Double) {
            self = Point(x: x + deltaX, y: y + deltaY)
        }
    }


> self表达式的语法

> self表达式 → **self**

> self表达式 → **self** **.** 标识符

> self表达式 → **self** [ 表达式 ]

> self表达式 → **self . init**


## 超类表达式


超类表达式可以让子类和超类相互访问，形式如下：

    super.`member name`

    super[`subscript index`]

    super.init（`initializer arguments`）



第一种形式用来访问超类的某个成员。第二种形式用来访问超类的子脚本实现（subscript implementation）。第三种用来访问该超类的初始设定式。


子类可以利用超类的实现，并通过使用超类表达式来实现它们的成员、下标和初始值。

> 超类表达式的语法

> 超类表达式 → 超类方法表达式 | 超类下标表达式 | 超类构造器表达式

> 超类方法表达式 → **super . **标识符

> 超类下标表达式 → **super [** 表达式 **]**

> 超类构造器表达式 → **super . init**

## 闭包表达式


闭包表达式可以创建一个闭包，就好像其他语言中的lambda或者匿名函数。跟函数声明一样，闭包包含了要执行的语句，接收作用域中的变量。形式如下：

    { (parameters) -> return type in
        statements
    }


闭包的参数声明跟函数的参数一样，具体请参见Function Declaration。


有好几种特殊形式，让闭包写起来更加简洁：


* 闭包可以省略参数和返回值的类型。如果省略了参数和参数类型，语句前的in也要省略。如果省略的类型不能被推断出来，那么就会抛出编译错误。


* 闭包可以省略参数名。如果省略参数名，它们会隐式地命名为：`$0`,`$1`,`$2`，以此类推。


如果闭包中只包含一个表达式，那么默认返回表达式的值。同时表达式的内容在进行类型推断的时候也会参考周围的表达式。


以下几个闭包表达式是等价的：

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


关于将闭包作为函数参数的更多内容，请参见：Function Call Expression。


闭包表达式可以明确指定从作用域中通过捕获列表来指定值。捕获列表是在参数列表前使用中括号加逗号分隔的形式组成的。一旦使用了捕获列表，即使省略了参数名，参数类型和返回值类型，也要使用in关键字。


捕获列表中的每一项都要标记为weak或unowned来捕获弱引用和无主引用。

    myFunction{ print（self.title） }                            
         // strong capture
    myFunction { [weak self] in     print（self!.title） }    
        // weak capture
    myFunction { [unowned self] in print（self.title） }  
        // unowned capture



在捕获列表中，你能给命名值绑定任意表达式。在闭包执行的时候表达式被计算并捕获。例如：

    // Weak capture of "self.parent" as "parent"
    myFunction { [weak parent = self.parent] in print(parent!.title) }


更多关于闭包表达式信息和例子，请参见 Closure Expressions。

> 闭包表达式的语法

> 闭包表达式 → **{** 闭包签名 可选 多条语句 **}**
> 闭包签名 → 参数子句 函数结果 可选 **in**
> 闭包签名 → 标识符列表 函数结果 可选 **in**
> 闭包签名 → 捕获列表 参数子句 函数结果 可选 **in**
> 
> 闭包签名 → 捕获列表 标识符列表 函数结果 可选 **in**
> 闭包签名 → 捕获列表 **in**
> 捕获列表 → **[** 捕获说明符 表达式 **]**
> 捕获说明符 → **weak** |**unowned** | **unowned(safe)** | **unowned(unsafe)**


# 隐式成员表达式

隐式成员表达式是一个访问类型成员变量的简写，例如枚举、类，通过上下文能够推断出隐式类型。形式如下：
    .member name


例子：

    var x = MyEnumeration.SomeValue
    x = .AnotherValue


> 隐式成员表达式的语法：

> 隐式成员表达式 → **.** 标识符


## 圆括号表达式

 
圆括号表达式由圆括号包裹、逗号分隔的子表达式列表组成。每个子表达式前面可以有一个可选标识符，由`:`分隔。形式如下：

    （identifier 1: expression 1, identifier 2: expression 2, ...）



圆括号表达式可以用来创建元祖,然后传递参数给函数。如果圆括号表达式中只有一个值，那么这个表达式的类型就是值的类型，例如表达式`(1)`的类型为`Int`不是`(Int)`。

> 圆括号表达式的语法

> 圆括号表达式 → **(**表达式元素列表 可选 **)**
> 
> 表达式元素列表 → 表达式元素 | 表达式元素 , 表达式元素列表
> 
> 表达式元素 → 表达式 | 标识符 **:** 表达式

## 通配符表达式


通配符表达式用来在赋值的时候显式地忽略某个值。比如下面的赋值语句中，`10`传递给`x`，`20`则被忽略。

     (x, _) = (10, 20)
     // x is 10, 20 is ignored



> 通配符表达式的语法

> 通配符表达式 → _


## 后缀表达式



后缀表达式由一个表达式后面加上一个后缀操作符或其他后缀语法组成。单纯从语法上讲，每个主表达式也是一个后缀表达式。


* ++ Increment
* -- Decrement

swift标准库提供了以下后缀操作符：
 
* ++ 自增
* -- 自减


更多关于这些操作符的使用信息，请参见“Basic Operators and Advanced Operators.”


> 后缀表达式的语法
> 
> 后置表达式 → 主表达式
> 
> 后置表达式 → 后置表达式 后置运算符
> 
> 后置表达式 → 函数调用表达式
> 
> 后置表达式 → 构造器表达式
> 
> 后置表达式 → 显示成员表达式
> 
> 后置表达式 → 后置self表达式
> 
> 后置表达式 → 动态类型表达式
> 
> 后置表达式 → 下标表达式
> 
> 后置表达式 → 强制取值表达式
> 
> 后置表达式 → 可选表达式

## 函数调用表达式


函数调用表达式由函数名后加圆括号组成，圆括号里面为逗号分隔的函数参数列表。形式如下：

     function name(argument value 1, argument value 2)


函数名称可以是任何返回值为函数类型的表达式。


如果函数声明中包含了参数名，那么函数调用时必须在参数值前加上参数名，并以分号分隔。这种函数调用表达式形式如下：

    function name(argument name 1: argument value 1, argument name 2: argument value 2)


函数调用表达式在括号后面可以包含闭包表达式的后缀闭包。后缀闭包会被当做函数的最后一个参数。下面两种写法相同：

     // someFunction takes an integer and a closure as its arguments
     
    someFunction(x, {$0 == 13})
    
    someFunction(x) {$0 == 13}


如果这个闭包是函数的唯一参数，那么圆括号可以省略。

     // someFunction takes a closure as its only argument
     
    myData.someMethod() {$0 == 13}
    
    myData.someMethod {$0 == 13}


> 函数调用表达式语法

> 函数调用表达式 → 后置表达式 圆括号表达式

> 函数调用表达式 → 后置表达式 圆括号表达式 可选 后置闭包
> 
> 后置闭包 → 闭包表达式


## 构造器表达式

构造器表达式提供类型初始化。形式如下：

     expression.init（initializer arguments）



你可以在函数调用表达式中使用构造器表达式来初始化一个类型的实例。构造器函数不像函数，它不能有返回值，例如：

    var x = SomeClass.someClassFunction // ok

    var y = SomeClass.init              // error


构造器表达式还可以用作对超类初始化函数的代理。

    class SomeSubClass: SomeSuperClass {
        init() {
            // subclass initialization goes here
            super.init()
        }
    }


> 构造器表达式的语法

> 构造器表达式 → 后置表达式 **. init**


## 显式成员表达式


显示成员表达式允许我们访问命名类型、元祖或模块的成员。它由元素、点（`.`）、成员的标识符三者组成。

    expression.member name

对于命名类型可作为类型定义或扩展的一部分。例如：

    class SomeClass {
        var someProperty = 42
    }
    let c = SomeClass()
    let y = c.someProperty  // Member access


元祖成员通过从零开始的有序整数隐式命名。例如：

    var t = (10, 20, 30)
    t.0 = t.1
    // Now t is (20, 20, 30)


模块成员可以访问模块的顶级（top-level）声明。


> 显示成员表达式的语法
> 显示成员表达式 → 后置表达式 . 十进制数字
> 显示成员表达式 → 后置表达式 . 标识符 泛型参数子句 可选


## 后缀self表达式


后缀self表达式由表达式或类型名，紧跟着`.self`组成。形式如下：

    expression.self
    type.self


第一种形式计算出表达式（`expression`）的值。例如`x.self`就等于`x`。


第二种形式计算出对应类型（`type`）的值。这种形式可以将某类型作为一个值来访问。例如，由于`SomeClass.self`等于`SomeClass`本身，所以你可以将其传给接受这种类型参数的函数或方法。


> 后缀self表达式的语法

> 后缀self表达式 → 后缀表达式 **. self**

## 动态类型表达式



动态类型（`dynamicType`）表达式由表达式和`.dynamicType`组成。形式如下：

    expression.dynamicType


表达式不能是类型的名字。整个动态类型表达式计算出表达式运行时的值，如下面的例子：

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


> 动态类型表达式的语法

> 动态类型表达式 → 后置表达式 **. dynamicType**

## 下标表达式


下标表达式提供用getter/setter方法访问下标声明。形式如下：

    expression[index expressions]
    

下标表达式可以通过传递下标参数（`index expressions`）计算getter的值，setter也可以通过同样的方式。


更多关于下标声明的信息，参见Protocol Subscript Declaration。

> 下标表达式语法：
> 
> 下标表达式 → 后置表达式 **[** 表达式列表 **]**

## 强制取值表达式


强制取值表达式用于对非空（not `nil`）的可选值进行强行拆包装。形式如下：

     expression!


上式中，如果一个`expression`的值不是`nil`，那么该可选值会被拆包装并返回相应的类型。否则抛出运行时错误。

> 强制取值表达式的语法：
> 
> 强制取值表达式 → 后置表达式 **!**

## 可选链式表达式


可选链式表达式提供一种在后缀表达式中使用可选值的简化的语法。形式如下：

    expression?


后缀`?`表达式就是简单的将所传参数作为可选值返回。


包含可选链式表达式的后缀表达式通过特殊的方式计算。如果可选链式表达式为nil，所有在此后缀表达式中的操作符都将被忽略，整个后缀表达式返回nil。如果不为nil，则可选链式表达式被拆包装，然后用于其他的后最表达式的计算。在这两种情况下，该后缀表达式仍然是一个可选类型。


如果一个包含可选链式表达式的后缀表达式嵌套在其他后缀表达式中，只有最外层的返回一个可选类型。下面例子中，当c不为nil时，它将被拆包然后用于.property和.performAction()的计算，整个表达式`c?.property.performAction() `拥有一个可选类型的值。

    var c: SomeClass?
    var result: Bool? = c?.property.performAction()


如果不使用可选链表达式，那么上面例子的代码等价于：

    if let unwrappedC = c {
        result = unwrappedC.property.performAction（）
    }


> 可选链表达式的语法

> 可选链表达式 → 后置表达式 ?