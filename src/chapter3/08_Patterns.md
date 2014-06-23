# Patterns
# 模式

A pattern represents the structure of a single value or a composite value. For example, the structure of a tuple ```(1, 2)``` is a comma-separated list of two elements. Because patterns represent the structure of a value rather than any one particular value, you can match them with a variety of values. For instance, the pattern (x, y) matches the tuple (1, 2) and any other two-element tuple. In addition matching a pattern with a value, you can extract part or all of a composite value and bind each part to a constant or variable name.

模式代表了单个值或者复合值的结构。例如，元组```(1, 2)```的结构是用逗号分隔的两个元素的列表。因为[to:由于]模式代表一种值的结构，而不是特定的某个值，你可以把模式和各种同类型的值进行匹配。比如，模式```(x, y)```可以匹配元组```(1, 2)```，以及任何含有两个元素的元组。除了将模式与一个[去掉“一个”]值匹配外，你可以从合成值中提取部分或全部，然后分别把各部分和一个常量或变量进行绑定。[to:并把各部分分别同常量或变量进行绑定]。

In Swift, patterns occur in variable and constant declarations (on their left-hand side), in ```for-in``` statements, and in ```switch``` statements (in their case labels). Although any pattern can occur in the case labels of a ```switch``` statement, in the other contexts, only wildcard patterns, identifier patterns, and patterns containing those two patterns can occur.

在Swift中，模式出现在变量和常量的声明（放在它们的左侧）、```for-in```语句及```switch```语句（放在其case标签内）中。尽管任何模式都可以出现在```switch```语句的case标签中，但在其他情况下，只有通配符模式、标识符模式和包含这两种模式的模式才能出现。

You can specify a type annotation for a wildcard pattern, an identifier pattern, and a tuple pattern to constraint the pattern to match only values of a certain type.

你可以为通配符模式、标识符模式和元组模式指定类型注释，用来限制这种模式只匹配某种类型的值。

> GRAMMAR OF A PATTERN
>
> pattern → wildcard-pattern­ type-annotation­ <sub>opt</sub>
> 
> pattern → identifier-pattern­ type-annotation­ <sub>opt</sub>
> 
> pattern → value-binding-pattern­
> 
> pattern → tuple-pattern­ type-annotation ­<sub>opt</sub>­
> 
> pattern → enum-case-pattern­
> 
> pattern → type-casting-pattern­
> 
> pattern → expression-pattern­

&nbsp;

> 模式语法
> 
> 模式 → 通配符模式 类型注解 <sub>可选</sub>
> 
> 模式 → 标识符模式 类型注解 <sub>可选</sub>
> 
> 模式 → 值绑定模式
> 
> 模式 → 元组模式 类型注解 <sub>可选</sub>
> 
> 模式 → 枚举用例模式
> 
> 模式 → 类型转换模式
> 
> 模式 → 表达式模式


## Wildcard Pattern
## 通配符模式

A wildcard pattern matches and ignores any value and consists of an underscore (_). Use a wildcard pattern when you don’t care about the values being matched against. For example, the following code iterates through the closed range ```1...3```, ignoring the current value of the range on each iteration of the loop:

通配符模式由一个下划线（_）组成，它会匹配并忽略任何值。当你不关心被匹配的值时，可以使用此模式。例如，下面这段代码对闭区间```1...3```进行了循环，并忽略了每次循环的区间当前值：

```
for _ in 1...3 {
    // Do something three times.
}
```

```
for _ in 1...3 {
    // 执行某操作3次.
}
```

> GRAMMAR OF A WILDCARD PATTERN
> 
> wildcard-pattern → _­

&nbsp;

> 通配符模式语法
> 
> 通配符模式 → _

## Identifier Pattern
## 标识符模式

An identifier pattern matches any value and binds the matched value to a variable or constant name. For example, in the following constant declaration, ```someValue``` is an identifier pattern that matches the value ```42``` of type ```Int```:

标识符模式匹配任何值，并把匹配的值绑定到一个变量或常量。例如，在下面的常量声明中，```someValue```是一个标识符模式，其匹配了类型是```Int```的值```42```。[to:它匹配了Int类型的值42]

```
let someValue = 42
```

```
let someValue = 42
```

When the match succeeds, the value ```42``` is bound (assigned) to the constant name ```someValue```.

当匹配成功时，值```42```被绑定（赋值）给了常量```someValue```

When the pattern on the left-hand side of a variable or constant declaration is an identifier pattern, the identifier pattern is implicitly a subpattern of a value-binding pattern.

当一个变量或常量声明的左边是标识符模式时，标识符模式是隐式的值绑定模式。[to:标识符模式是值绑定模式的隐式子模式]

> GRAMMAR OF AN IDENTIFIER PATTERN
> 
> identifier-pattern → identifier­

&nbsp;

> 标识符模式语法
>
> 标识符模式 → 标识符

## Value-Binding Pattern
## 值绑定模式

A value-binding pattern binds matched values to variable or constant names. Value-binding patterns that bind a matched value to the name of a constant begin with the keyword ```let```; those that bind to the name of variable begin with the keyword ```var```.

值绑定模式绑定匹配的值到一个变量或常量[to:值绑定模式把匹配的值绑定到一个变量或常量上]。绑定匹配值给常量时[to:把匹配值绑定给常量时]，以关键字```let```开头；绑定给变量时，则使用关键字```var```。

Identifiers patterns within a value-binding pattern bind new named variables or constants to their matching values. For example, you can decompose the elements of a tuple and bind the value of each element to a corresponding identifier pattern.

包含在值绑定模式中的标识符模式，会绑定新的变量或常量到其匹配的值[to:会把新命名的变量或常量绑定到它们匹配的值]。例如，你可以分解一个元组的元素，并把每个元素绑定到相应的标识符模式中。

```
let point = (3, 2)
switch point {
    // Bind x and y to the elements of point.
case let (x, y):
    println("The point is at (\(x), \(y)).")
}
// prints "The point is at (3, 2)."
```

```
let point = (3, 2)
switch point {
    // 将x，y分别绑定到常量point的元素3，2。
case let (x, y):
    println("The point is at (\(x), \(y)).")
}
// prints "The point is at (3, 2)."
```

In the example above, ```let``` distributes to each identifier pattern in the tuple pattern ```(x, y)```. Because of this behavior, the ```switch``` cases ```case let (x, y):``` and ```case (let x, let y):``` match the same values.

在上面的例子中，```let```将元组模式```(x, y)```分配到各个标识符模式[to:let把元素分配给元组模式(x,y)的相应标识符模式]。因为这种行为[to:正是由于这种行为]，```switch```语句中的```case let (x, y):```和```case (let x, let y):```匹配的值是一样的。

> GRAMMAR OF A VALUE-BINDING PATTERN
> 
> value-binding-pattern → var­ pattern­  let ­pattern­

&nbsp;

> 值绑定模式语法
> 
> 值绑定模式 → var 模式 | let 模式

## Tuple Pattern
## 元组模式

A tuple pattern is a comma-separated list of zero or more patterns, enclosed in parentheses. Tuple patterns match values of corresponding tuple types.

元组模式是被一对圆括号包围、并以逗号分隔的列表，列表中可以包含零或多个模式[to:元组模式是被一对圆括号包围，含有零或多个模式，并用逗号分隔的列表]。元组模式会匹配相应元组类型的值。

You can constrain a tuple pattern to match certain kinds of tuple types by using type annotations. For example, the tuple pattern ```(x, y): (Int, Int)``` in the constant declaration ``` let (x, y): (Int, Int) = (1, 2)```  matches only tuple types in which both elements are of type ``` Int``` . To constrain only some elements of a tuple pattern, provide type annotations directly to those individual elements. For example, the tuple pattern in ``` let (x: String, y)```  matches any two-element tuple type, as long as the first element is of type ``` String``` .

你可以使用类型注释来限制一个元组模式仅匹配某种类型的元组。例如，在常量声明```let (x, y): (Int, Int) = (1, 2)```中的元组模式```(x, y): (Int, Int)```只匹配两个元素都是```Int```类型的元组。如果仅需要限制元组模式中的某几个元素，直接对这几个元素提供类型注释即可。例如，在```let (x: String, y)```中的元组模式，将匹配[增加“任意”]包含两个元素且第一个元素类型是```String```的任意[去掉“任意”]元组。

When a tuple pattern is used as the pattern in a ```for-in``` statement or in a variable or constant declaration, it can contain only wildcard patterns, identifier patterns, or other tuple patterns that contain those. For example, the following code isn’t valid because the element ```0``` in the tuple pattern ```(x, 0)``` is an expression pattern:

当元组模式["被用在"to“用于”]```for-in```语句、变量或常量声明中时，它只可以包含通配符模式、标识符模式或者其他包含这两种模式的模式。例如，下面这段代码是不正确的，因为元组模式```(x, 0)```中的元素```0```是一个[去掉“一个”]表达式模式：

```
let points = [(0, 0), (1, 0), (1, 1), (2, 0), (2, 1)]
// This code isn't valid.
for (x, 0) in points {
    /* ... */
}
```

```
let points = [(0, 0), (1, 0), (1, 1), (2, 0), (2, 1)]
// 下面的代码是不正确的.
for (x, 0) in points {
    /* ... */
}
```

The parentheses around a tuple pattern that contains a single element have no effect. The pattern matches values of that single element’s type. For example, the following are equivalent:

对于只包含一个元素的元组，包围元组的圆括号是不起作用的。模式会匹配该单个元素的类型。例如，下面的不同写法是等效的["等效的"to“等价的”]：

```
let a = 2        // a: Int = 2
let (a) = 2      // a: Int = 2
let (a): Int = 2 // a: Int = 2
```

```
let a = 2        // a: Int = 2
let (a) = 2      // a: Int = 2
let (a): Int = 2 // a: Int = 2
```

> GRAMMAR OF A TUPLE PATTERN
>
> tuple-pattern → (­ tuple-pattern-element-list­ <sub>opt</sub> )­
> 
> tuple-pattern-element-list → tuple-pattern-element­  | tuple-pattern-element­ ,­ tuple-pattern-element-list­
> 
> tuple-pattern-element → pattern­

&nbsp;

> 元组模式语法
> 
> 元组模式 → ( 元组模式元素列表 <sub>可选</sub> )
> 
> 元组模式元素列表 → 元组模式元素 | 元组模式元素 , 元组模式元素列表
> 
> 元组模式元素 → 模式

## Enumeration Case Pattern
## 枚举用例模式

An enumeration case pattern matches a case of an existing enumeration type. Enumeration case patterns appear only in ```switch``` statement case labels.

枚举用例模式匹配现有枚举类型的某种用例。枚举用例模式仅在```switch```语句的case标签中出现。

If the enumeration case you’re trying to match has any associated values, the corresponding enumeration case pattern must specify a tuple pattern that contains one element for each associated value. For an example that uses a ```switch``` statement to match enumeration cases containing associated values, see [Associated Values]().

如果你准备匹配的枚举用例有任何关联的值，则相应的枚举用例模式必须指定一个包含每个关联值元素的元组模式。使用```switch```语句来匹配包含关联值的枚举用例的例子，请参阅[关联值]().

> GRAMMAR OF AN ENUMERATION CASE PATTERN
> 
> enum-case-pattern → type-identifier ­opt­ .­ enum-case-name­ tuple-pattern­ <sub>opt</sub>­

&nbsp;

> 枚举用例模式语法
> 
> 枚举用例模式 → 类型标识 可选 . 枚举的case名 元组模式 <sub>可选</sub>

## Type-Casting Patterns
## 类型转换模式

There are two type-casting patterns, the ```is``` pattern and the ```as``` pattern. Both type-casting patterns appear only in ```switch``` statement case labels. The ```is``` and ```as``` patterns have the following form:

有两种类型转换模式，分别是```is```模式和```as```模式。这两种模式均["均"to"都"]只出现在```switch```语句的case标签中。```is```模式和```as```模式有以下形式：

> is type
> 
> pattern as type

&nbsp;

> ```is``` type
> 
> pattern ```as``` type

The ```is``` pattern matches a value if the type of that value at runtime is the same as the type specified in the right-hand side of the ```is``` pattern—or a subclass of that type. The ```is``` pattern behaves like the ```is``` operator in that they both perform a type cast but discard the returned type.

如果一个值的类型在运行时（runtime）和```is```模式右边所指定的类型（或者那个类型的子类型）一致，```is```模式将会匹配这个值。```is```模式类似```is```操作符，它们都进行类型转换，但是抛弃了返回的类型。

The ```as``` pattern matches a value if the type of that value at runtime is the same as the type specified in the right-hand side of the ```as``` pattern—or a subclass of that type. If the match succeeds, the type of the matched value is cast to the pattern specified in the left-hand side of the ```as``` pattern.

如果一个值的类型在运行时（runtime）和```as```模式右边所指定的类型（或者那个类型的子类型）一致，```as```模式将会匹配这个值。一旦匹配成功，匹配值的类型被转换成```as```模式左边所指定的模式。

For an example that uses a ```switch``` statement to match values with ```is``` and ```as``` patterns, see [Type Casting for Any and AnyObject]().

关于使用```switch```语句来匹配```is```模式和```as```模式值的例子，请参阅[Type Casting for Any and AnyObject]()。

> GRAMMAR OF A TYPE CASTING PATTERN
>
> type-casting-pattern → is-pattern­  as-pattern­
> is-pattern → is­ type­
> as-pattern → pattern­ as ­type­

&nbsp;

> 类型转换模式语法
>
> 类型转换模式 → is模式 | as模式
> is模式 → is 类型
> as模式 → 模式 as 类型

## Expression Pattern
## 表达式模式

An expression pattern represents the value of an expression. Expression patterns appear only in ```switch``` statement case labels.

表达式模式代表了一个表达式的值。该模式只出现在```switch```语句的case标签中。

The expression represented by the expression pattern is compared with the value of an input expression using the Swift standard library ```~=``` operator. The matches succeeds if the ```~=``` operator returns ```true```. By default, the ```~=``` operator compares two values of the same type using the ```==``` operator. It can also match an integer value with a range of integers in an ```Range``` object, as the following example shows:

由表达式模式所代表的表达式会使用Swift标准库中的```~=```操作符与输入表达式的值进行比较。如果```~=```操作符返回```true```，则匹配成功。默认情况下，```~=```操作符使用```==```操作符来比较两个相同类型的值。它也可以匹配一个整数值与一个```Range```对象中的整数范围，正如下面这个例子所示：

```
let point = (1, 2)
switch point {
case (0, 0):
    println("(0, 0) is at the origin.")
case (-2...2, -2...2):
    println("(\(point.0), \(point.1)) is near the origin.")
default:
    println("The point is at (\(point.0), \(point.1)).")
}
// prints "(1, 2) is near the origin."
```

```
let point = (1, 2)
switch point {
case (0, 0):
    println("(0, 0) is at the origin.")
case (-2...2, -2...2):
    println("(\(point.0), \(point.1)) is near the origin.")
default:
    println("The point is at (\(point.0), \(point.1)).")
}
// prints "(1, 2) is near the origin."
```

You can overload the ```~=``` operator to provide custom expression matching behavior. For example, you can rewrite the above example to compare the point expression with a string representations of points.

你可以重载```~=```操作符来提供自定义的表达式匹配行为。例如，你可以重写上面的例子来比较使用字符串所表达的点[你可以使用point的字符串形式来比较point表达式]。

```
// Overload the ~= operator to match a string with an integer
func ~=(pattern: String, value: Int) -> Bool {
    return pattern == "\(value)"
}
switch point {
case ("0", "0"):
    println("(0, 0) is at the origin.")
case ("-2...2", "-2...2"):
    println("(\(point.0), \(point.1)) is near the origin.")
default:
    println("The point is at (\(point.0), \(point.1)).")
}
// prints "(1, 2) is near the origin."
```

```
// 重载 ~= 操作符让整数能匹配字符串
func ~=(pattern: String, value: Int) -> Bool {
    return pattern == "\(value)"
}
switch point {
case ("0", "0"):
    println("(0, 0) is at the origin.")
case ("-2...2", "-2...2"):
    println("(\(point.0), \(point.1)) is near the origin.")
default:
    println("The point is at (\(point.0), \(point.1)).")
}
// prints "(1, 2) is near the origin."
```

> GRAMMAR OF AN EXPRESSION PATTERN
>
> expression-pattern → expression­

&nbsp;

> 表达式模式语法
> 
> 表达式模式 → 表达式

