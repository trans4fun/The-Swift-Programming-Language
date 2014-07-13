# Attributes

# 特性

*Attributes* provide more information about a declaration or type. There are two kinds of attributes in Swift, those that apply to declarations and those that apply to types. For instance, the `required` attribute—when applied to a designated or convenience initializer declaration of a class—indicates that every subclass must implement that initializer. And the `noreturn` attribute—when applied to a function or method type—indicates that the function or method doesn’t return to its caller.

*特性* 为声明和类型提供了更多的信息。在Swift中有两种类型的特性，一种用于修饰声明，另一种用于修饰类型。比如，`required`特性——当被用来修饰一个类的预设构造函数声明或者便利构造函数声明时——表明其所有的子类都必须实现这个构造函数。`noreturn`特性——当修饰函数或者方法类型时——表明这个函数或者方法不会返回任何值给其调用者。

You specify an attribute by writing the `@` symbol followed by the attribute’s name and any arguments that the attribute accepts:

```
  @attribute name
  @attribute name(attribute arguments)
```

你可以通过`@`符号以及紧随其后的特性名称和该特性可以接受的参数来使用特性。

```
  @attribute name
  @attribute name(attribute arguments)
```
	
Some declaration attributes accept arguments that specify more information about the attribute and how it applies to a particular declaration. These *attribute arguments* are enclosed in parentheses, and their format is defined by the attribute they belong to.

有些声明特性可以通过给定参数来补充该特性相关的更多信息，并说明该特性将如何应用于这个声明中。这些`特性参数`写在小括号里面，他们的具体格式需要根据他们所属的特性来确定。

## Declaration Attributes

## 声明特性

You can apply a declaration attribute to declarations only. However, you can also apply the `noreturn` attribute to a function or method *type*.

声明特性只能描述声明。不过你还是可以使用`noreturn`特性来描述函数或者方法*类型*。

`assignment`
> Apply this attribute to functions that overload a compound assignment operator. Functions that overload a compound assignment operator must mark their initial input parameter as `inout`. For an example of how to use the assignment attribute, see [Compound Assignment Operators](#).

`assignment`
> 这个特性用于描述重载了复合赋值运算符的函数。一个重载了复合赋值运算符的函数必须将它的初始化输入参数标记为`inout`.关于如何使用assigment特性请查看[符合赋值运算符](#)中的一个例子。

`class_protocol`
> Apply this attribute to a protocol to indicate that the protocol can be adopted by class types only.

> If you apply the `objc` attribute to a protocol, the `class_protocol` attribute is implicitly applied to that protocol; there’s no need to mark the protocol with the `class_protocol` attribute explicitly.

`class_protocol`
> 这个特性用于描述协议，它表明被修饰的协议只能被类使用[//todo adopted]。

> 如果一个协议已经添加了`objc`特性，那么`class_protocol`特性就已经被隐形地添加在这个协议上了，不需要再显性地添加一次。

`exported`
> Apply this attribute to an import declaration to export the imported module, submodule, or declaration from the current module. If another module imports the current module, that other module can access the items exported by the current module.

`exported`
> 这个特性被用于修饰导入声明。当一个导入声明具有该特性时，所有通过该声明导入的的模块，子模块或者声明都可以被导出。如果另一个模块导入了这个模块，那么那个模块可以访问所有被这个模块导出的项。

`final`
> Apply this attribute to a class or to a property, method, or subscript member of a class. It’s applied to a class to indicate that the class can’t be subclassed. It’s applied to a property, method, or subscript of a class to indicate that that class member can’t be overridden in any subclass.

`final`
> 这个特性用于描述类或者类的属性、方法、或者下标上。如若一个类具有该特性，则表明这个类不能被继承。如果一个类的属性、方法或者下标具有该特性，则表明这个类的成员不能被任何子类覆盖。

`lazy`
> Apply this attribute to a stored variable property of a class or structure to indicate that the property’s initial value is calculated and stored at most once, when the property is first accessed. For an example of how to use the `lazy` attribute, see [Lazy Stored Properties](#).

`lazy`
> 如果一个类或者结构体的存储变量属性具有该特性，则这个属性的初始值最多只被计算和存储一次，且这一次的计算和存储发生在第一次被访问时。查看[懒惰存储属性](#)中给出的关于如何使用`lazy`的例子。

`noreturn`
> Apply this attribute to a function or method declaration to indicate that the corresponding type of that function or method, `T`, is `@noreturn T`. You can mark a function or method type with this attribute to indicate that the function or method doesn’t return to its caller.

> You can override a function or method that is not marked with the `noreturn` attribute with a function or method that is. That said, you can’t override a function or method that is marked with the `noreturn` attribute with a function or method that is not. Similar rules apply when you implement a protocol method in a conforming type.

`noreturn`
> 可以通过将这个特性应用在函数或者方法声明中来指定这个函数或者方法，`T`，是`@noreturn T`类型。你可以通过使用这个特性来标记函数或者方法，借此来表明这个函数或者方法不返回任何值给它的调用者。

> 你可以使用一个标记了这个特性的函数或者方法来覆盖一个没有标记过这个特性的函数或者方法，但是反过来不行。同样的，当你要实现一个协议方法时，也需要遵循这个规则。

`NSCopying`
> Apply this attribute to a stored variable property of a class. This attribute causes the property’s setter to be synthesized with a *copy* of the property’s value—returned by the `copyWithZone` method—instead of the value of the property itself. The type of the property must conform to the `NSCopying` protocol.

> The `NSCopying` attribute behaves in a way similar to the Objective-C `copy` property attribute.

`NSCopying`
> 这个特性用于修饰一个类的储存变量属性。该特性将使得这个类的属性的setter方法与这个属性的返回值的*副本*合成——通过`copyWithZone`方法进行返回——而不是这个属性值本身。这个属性值的类型必须遵循`NSCopying`协议。

> `NSCopying`特性与Objective-C中的`copy`属性特性类似。

`NSManaged`
> Apply this attribute to a stored variable property of a class that inherits from `NSManagedObject` to indicate that the storage and implementation of the property are provided dynamically by Core Data at runtime based on the associated entity description.

`NSManaged`
> 这个特性用于修饰继承了`NSManagedObject`的类的成员，通过该特性来表明这个成员的存储和实现由Core Data在运行时根据相关实体描述来动态地提供。

`objc`
> Apply this attribute to any declaration that can be represented in Objective-C—for example, non-nested classes, protocols, properties and methods (including getters and setters) of classes and protocols, initializers, deinitializers, and subscripts. The `objc` attribute tells the compiler that a declaration is available to use in Objective-C code.

> If you apply the `objc` attribute to a class or protocol, it’s implicitly applied to the members of that class or protocol. The compiler also implicitly adds the `objc` attribute to a class that inherits from another class marked with the `objc` attribute. Protocols marked with the `objc` attribute can’t inherit from protocols that aren’t.

> The `objc` attribute optionally accepts a single attribute argument, which consists of an identifier. Use this attribute when you want to expose a different name to Objective-C for the entity the `objc` attribute applies to. You can use this argument to name classes, protocols, methods, getters, setters, and initializers. The example below exposes the getter for the enabled property of the `ExampleClass` to Objective-C code as `isEnabled` rather than just as the name of the property itself.

```
	@objc
	class ExampleClass {
    	var enabled: Bool {
    	@objc(isEnabled) get {
        	// Return the appropriate value
    	}
    	}
	}
```

`objc`
> 这个特性用于描述任何可以在Objective-C中表示的声明，如非嵌套类，协议，类和协议的属性和方法（包括getter和setter），构造函数，析构函数和下标。`objc`特性告诉编译器该声明可以在Objective-C的代码中被使用。

> 如果一个类或者协议具有`objc`特性，那么这个类或者协议的所有成员都将隐形地具有`objc`特性。编译器甚至会隐形地添加`objc`特性给具有`objc`特性的类的子类。被标记`objc`特性的协议不能继承没有被标记`objc`特性的协议。

> `objc`特性可选地接收一个标识符作为参数。你就可以使用这个特性参数让被标记的对象对Objective-C暴露一个不一样的名字。你可以使用这个参数来重新命名类，协议，方法，getter，setter和构造函数。下面的例子通过给定特性参数使得类`ExampleClass`的enabled这个属性以`isEnabled`这个名字暴露给Objective-C.

```
	@objc
	class ExampleClass {
    	var enabled: Bool {
    	@objc(isEnabled) get {
        	// 返回合适的值
    	}
    	}
	}
```

`optional`
> Apply this attribute to a protocol’s property, method, or subscript members to indicate that a conforming type isn’t required to implement those members.

> You can apply the `optional` attribute only to protocols that are marked with the `objc` attribute. As a result, only class types can adopt and conform to a protocol that contains optional member requirements. For more information about how to use the `optional` attribute and for guidance about how to access optional protocol members—for example, when you’re not sure whether a conforming type implements them—see [Optional Protocol Requirements](#).

`optional` 

> 这个特性用于描述协议的属性，方法和下标，以此来表明遵循了该协议的类型，只需要可选地实现这些被标记的成员。

> 这个特性只能被用于描述具有`objc`特性的协议。也就是说，只有类才能接受和遵循一个具有optional特性成员的协议。更多关于如何使用`optional`特性，以及对于一个遵循了具有`optional`特性的协议的类型，在无法明确它实现了哪些可选成员的情况下，如何正确地读取其可选成员的问题，请参考[可选协议要求](#)。

`required`
> Apply this attribute to a designated or convenience initializer of a class to indicate that every subclass must implement that initializer.

> Required designated initializers must be implemented explicitly. Required convenience initializers can be either implemented explicitly or inherited when the subclass directly implements all of the superclass’s designated initializers (or when the subclass overrides the designated initializers with convenience initializers).

`required`
> 通过为一个类的预设构造函数或者便利构造函数添加该特性来表明这个类的每一个子类都必须实现这个构造函数。

> 具有该特性的预设构造函数必须被显性地实现。具有该特性的便利构造函数可以被显性地实现，或者当子类直接实现了所有父类的预设构造函数时（或者子类使用便利构造函数重写了预设构造函数），可以直接继承这个便利构造函数。

### Declaration Attributes Used by Interface Builder

## 在Interface Builder中使用声明特性

Interface Builder attributes are declaration attributes used by Interface Builder to synchronize with Xcode. Swift provides the following Interface Builder attributes: `IBAction`, `IBDesignable`, `IBInspectable`, and `IBOutlet`. These attributes are conceptually the same as their Objective-C counterparts.

Interface Builder特性是Interface Builder用来和Xcode同步的声明特性。Swift提供了以下几种Interface Builder特性: `IBAction`，`IBDesignable`，`IBInspectable`和`IBOutlet`。这些特性在概念上和Objective-C中对应的特性是一样的。

You apply the `IBOutlet` and `IBInspectable` attributes to property declarations of a class. You apply the `IBAction` attribute to method declarations of a class and the `IBDesignable` attribute to class declarations.

`IBOutlet`和`IBInspectable`特性用于描述类的属性声明，`IBAction`特性用于描述类的方法声明而`IBDesignable`用于描述类的声明。

## Type Attributes

## 类型特性

You can apply type attributes to types only. However, you can also apply the `noreturn` attribute to a function or method *declaration*.

类型特性只能描述类型。尽管如此，你还是可以使用`noreturn`特性去修饰函数和方法的声明。

`auto_closure`
> This attribute is used to delay the evaluation of an expression by automatically wrapping that expression in a closure with no arguments. Apply this attribute to a function or method type that takes no arguments and that returns the type of the expression. For an example of how to use the `auto_closure` attribute, see [Function Type](#).

`auto_closure`
> 这个特性通过自动地将表达式包裹在一个没有参数的闭包中来延迟表达式的求值。将该特性用于描述不带任何参数的函数和方法，而这些函数和方法返回表达式的类型。关于如何使用`auto_closure`特性，参考[函数类型](#)中的例子。

`noreturn`
> Apply this attribute to the type of a function or method to indicate that the function or method doesn’t return to its caller. You can also mark a function or method declaration with this attribute to indicate that the corresponding type of that function or method, `T`, is `@noreturn T`.

`noreturn`
> 使用这个特性来描述函数或者方法，以此表明该函数或者方法不返回任何值给它的调用者。你也可以使用这个特性来标记函数或者方法声明，借此来表明这个函数或者方法，`T`，是`@noreturn T`类型。

## GRAMMAR OF AN ATTRIBUTE

## 特性语法总结

> attribute → @attribute-nameattribute-argument-clauseopt

> attribute-name → identifier

> attribute-argument-clause → (balanced-tokensopt)

> attributes → attributeattributesopt

> balanced-tokens → balanced-tokenbalanced-tokensopt

> balanced-token → (balanced-tokensopt)

> balanced-token → [balanced-tokensopt]

> balanced-token → {balanced-tokensopt}

> balanced-token → Any identifier, keyword, literal, or operator

> balanced-token → Any punctuation except (, ), [, ], {, or }


