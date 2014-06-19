# Generic Parameters and Arguments
# 泛型参数


This chapter describes parameters and arguments for generic types, functions, and initializers. When you declare a generic type, function, or initializer, you specify the type parameters that the generic type, function, or initializer can work with. These type parameters act as placeholders that are replaced by actual concrete type arguments when an instance of a generic type is created or a generic function or initializer is called.

本章节介绍泛型类型、函数、初始构造器的参数。当你在声明泛型类型、函数或者初始化构造器时，你指定了它们能够使用的类型参数。这些类型参数起到了占位符的作用，在泛型类型的实例创建或者泛型方法、初始化构造器调用时，它们会被替换为实际的参数。

For an overview of generics in Swift, see [Generics](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Generics.html#//apple_ref/doc/uid/TP40014097-CH26-XID_234).

关于Swift泛型的概述，可以详见[泛型](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Generics.html#//apple_ref/doc/uid/TP40014097-CH26-XID_234)。

## Generic Parameter Clause
## 泛型形参句式

A generic parameter clause specifies the type parameters of a generic type or function, along with any associated constraints and requirements on those parameters. A generic parameter clause is enclosed in angle brackets (<>) and has one of the following forms:

泛型参数句式指定了泛型类型或函数的参数类型，以及与这些参数相关的约束、依赖条件。泛型参数句式的内容用一对尖括号包围，并且是以下形式中的一种：

```
<generic parameter list>
<generic parameter list where requirements>
```
The generic parameter list is a comma-separated list of generic parameters, each of which has the following form:
泛型参数列表是用逗号分隔的一组参数，其中的每一个都类似以下的形式：

```
type parameter: constraint
```

A generic parameter consists of a type parameter followed by an optional constraint. A type parameter is simply the name of a placeholder type (for instance, T, U, V, KeyType, ValueType, and so on). You have access to the type parameters (and any of their associated types) in the rest of the type, function, or initializer declaration, including in the signature of the function or initializer.

泛型参数由类型形参组成，紧跟其后的是是一个可选的约束条件。类型形参只是一个占位符类型的名称（比如：T、U、V、KeyType、ValueType等）。You have access to the type parameters (and any of their associated types) in the rest of the type, function, or initializer declaration, including in the signature of the function or initializer.

The constraint specifies that a type parameter inherits from a specific class or conforms to a protocol or protocol composition. For instance, in the generic function below, the generic parameter T: Comparable indicates that any type argument substituted for the type parameter T must conform to the Comparable protocol.

约束条件指定了类型形参是继承自特定的类、符合某个协议或者协议的组件部分。比如，在下面的泛型函数中，泛型形参T: Comparable表明替换泛型类型形参的任何类型实参都必须符合Comparable协议。

```
func simpleMin<T: Comparable>(x: T, y: T) -> T {
    if x < y {
        return y
    }
    return x
}
```

Because Int and Double, for example, both conform to the Comparable protocol, this function accepts arguments of either type. In contrast with generic types, you don’t specify a generic argument clause when you use a generic function or initializer. The type arguments are instead inferred from the type of the arguments passed to the function or initializer.

比如，Int与Double都符合Comparable协议，所以这个函数接受任意一种实参类型。与泛型类型形参相反的是，当使用泛型方式或者初始构造器时，无需指定泛型实参的句式，实参由传入函数或初始化构造器的实际类型推断得出。


```
simpleMin(17, 42) // T被推断是Int
simpleMin(3.14159, 2.71828) // T被推断是Double
```

## Where Clauses
## Where 句式

You can specify additional requirements on type parameters and their associated types by including a where clause after the generic parameter list. A where clause consists of the keyword where, followed by a comma-separated list of one or more requirements.

通过在泛型形参列表之后引入where句式，在类型形参及相关的类型上定义额外的依赖条件。where句式由where关键字和紧随其后的由逗号分隔的一个或多个依赖条件组成。

The requirements in a where clause specify that a type parameter inherits from a class or conforms to a protocol or protocol composition. Although the where clause provides syntactic sugar for expressing simple constraints on type parameters (for instance, T: Comparable is equivalent to T where T: Comparable and so on), you can use it to provide more complex constraints on type parameters and their associated types. For instance, you can express the constraints that a generic type T inherits from a class C and conforms to a protocol P as <T where T: C, T: P>.

where句式的依赖条件指定了类型形参是继承自特定的类、符合某个协议或者协议的组成部分。尽管where句式提供了语法糖来简化表达类型形参的约束条件（比如，T: Comparable等同于T where T: Comparable等），但仍可以在类型形参和相关类型上提供复杂的约束条件。比如：泛型类型T继承自类C且符合协议P可以表达为```<T where T: C, T: P>```。

As mentioned above, you can constrain the associated types of type parameters to conform to protocols. For example, the generic parameter clause <T: Generator where T.Element: Equatable> specifies that T conforms to the Generator protocol and the associated type of T, T.Element, conforms to the Equatable protocol (T has the associated type Element because Generator declares Element and T conforms to Generator).

如上所述，可以约束类型形参的相关类形符合特定的协议。比如：泛型参数句式```<T: Generator where T.Element: Equatable>```指定了T符合Generator协议，且T的Element类型符合Equatable协议（T有关联系的Element类型是因为Generator协议声明了Element，而T符合Generator协议）。

You can also specify the requirement that two types be identical, using the == operator. For example, the generic parameter clause <T: Generator, U: Generator where T.Element == U.Element> expresses the constraints that T and U conform to the Generator protocol and that their associated types must be identical.
你也可以用```==```运符符指定两种类型完全相等的依赖条件。比如，泛型形参句式```<T: Generator, U: Generator where T.Element == U.Element>```表明T和U符合Generator协议，并且他们关联的类型必须完全相等的约束条件。

Any type argument substituted for a type parameter must meet all the constraints and requirements placed on the type parameter.
所有实参在替换类型形参时必须实现所有的约束和依赖条件。

You can overload a generic function or initializer by providing different constraints, requirements, or both on the type parameters in the generic parameter clause. When you call an overloaded generic function or initializer, the compiler uses these constraints to resolve which overloaded function or initializer to invoke.
通过在泛型参数句式中为类型形参定义不同的约束条件、依赖条件来实现泛型函数、初始化构造器的重载。当调用重载的泛型函数或初始化构造器时，编译器会使用这些约束条件来实现它们的调用。

You can subclass a generic class, but the subclass must also be a generic class.
泛型类可以子类化，但子类也必须是一个泛型类。

> **GRAMMAR OF A GENERIC PARAMETER CLAUSE**

> generic-parameter-clause → <­generic-parameter-list­requirement-clause­opt­>­
> generic-parameter-list → generic-parameter­  generic-parameter­,­generic-parameter-list­
> generic-parameter → type-name­
> generic-parameter → type-name­:­type-identifier­
> generic-parameter → type-name­:­protocol-composition-type­
> requirement-clause → where­requirement-list­
> requirement-list → requirement­  requirement­,­requirement-list­
> requirement → conformance-requirement­  same-type-requirement­
> conformance-requirement → type-identifier­:­type-identifier­
> conformance-requirement → type-identifier­:­protocol-composition-type­
> same-type-requirement → type-identifier­==­type-identifier­


## Generic Argument Clause
## 泛型实参句式

A generic argument clause specifies the type arguments of a generic type. A generic argument clause is enclosed in angle brackets (<>) and has the following form:

泛型实参句式指定了泛型类型的类型实参。它由一对尖括号包围，形式如下：

```
<generic argument list>
```

The generic argument list is a comma-separated list of type arguments. A type argument is the name of an actual concrete type that replaces a corresponding type parameter in the generic parameter clause of a generic type. The result is a specialized version of that generic type. As an example, the Swift standard library defines a generic dictionary type as:

泛型实参列表是由一组逗号分隔组成的类型实参

```
struct Dictionary<KeyType: Hashable, ValueType>: Collection, DictionaryLiteralConvertible {
    /* ... */
}
```








