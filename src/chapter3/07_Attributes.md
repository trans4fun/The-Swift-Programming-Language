# Attributes

# 属性

*Attributes* provide more information about a declaration or type. There are two kinds of attributes in Swift, those that apply to declarations and those that apply to types. For instance, the `required` attribute—when applied to a designated or convenience initializer declaration of a class—indicates that every subclass must implement that initializer. And the `noreturn` attribute—when applied to a function or method type—indicates that the function or method doesn’t return to its caller.

*属性* 为声明和类型提供了更多的信息。在Swift中有两种类型的属性，一种应用在声明中，另一种应用于类型。比如，`required`属性——当被应用在一个类的预设初构造函数或者便利构造函数中时——表明了其所有的子类都必须实现这个构造函数。`noreturn`属性——当被应用在函数或者方法类型中时——表明这个函数或者方法不会返回任何值给调用者。

You specify an attribute by writing the `@` symbol followed by the attribute’s name and any arguments that the attribute accepts:

```
  @attribute name
  @attribute name(attribute arguments)
```

你可以通过`@`符号以及紧随其后的属性名称和该属性接受的参数来指定属性。

```
  @属性名称
  @属性名称(属性参数)
```
	
Some declaration attributes accept arguments that specify more information about the attribute and how it applies to a particular declaration. These *attribute arguments* are enclosed in parentheses, and their format is defined by the attribute they belong to.

有些声明属性可以通过给定参数来指定该属性相关的更多信息，以及描述该属性如何应用于这个声明中。

## Declaration Attributes

## 声明属性

You can apply a declaration attribute to declarations only. However, you can also apply the `noreturn` attribute to a function or method *type*.

你只能将声明属性应用在声明中。不过你还是可以将`noreturn`属性应用在函数或者方法*类型*中。

`assignment`
> Apply this attribute to functions that overload a compound assignment operator. Functions that overload a compound assignment operator must mark their initial input parameter as `inout`. For an example of how to use the assignment attribute, see [Compound Assignment Operators](#).

`assignment`
> 这个属性应用于那些重载了复合赋值运算符的函数上。 一个重载了复合赋值运算符必须将它的初始化输入参数标记为`inout`.查看[符合赋值运算符]中关于如何使用assigment属性的一个例子。

`class_protocol`
> Apply this attribute to a protocol to indicate that the protocol can be adopted by class types only.

> If you apply the `objc` attribute to a protocol, the `class_protocol` attribute is implicitly applied to that protocol; there’s no need to mark the protocol with the `class_protocol` attribute explicitly.

`class_protocol`
> 当这个属性被应用在协议上时，它表明这个协议只能被类使用。

> 如果一个协议被应用了`objc`属性，那么`class_protocol`属性就被隐形地添加在这个协议上了，不需要再显性地添加一次。

`exported`
> Apply this attribute to an import declaration to export the imported module, submodule, or declaration from the current module. If another module imports the current module, that other module can access the items exported by the current module.

`exported`
> 通过将这个属性应用给一个导入声明，使得当前模块中被导入进来的模块，子模块或者声明可以被导出。如果另一个模块导入了这个模块，那么这个模块可以访问所有被这个模块导出的项。

`final`
> Apply this attribute to a class or to a property, method, or subscript member of a class. It’s applied to a class to indicate that the class can’t be subclassed. It’s applied to a property, method, or subscript of a class to indicate that that class member can’t be overridden in any subclass.

`final`
> 这个属性被应用在一个类或者一个类的属性、方法、或者子脚本上。如果应用在类上，则表明这个类不能被继承。如果被应用在一个类的属性、方法或者子脚本上，则表明这个类的成员不能被任何子类覆盖。

`lazy`
> Apply this attribute to a stored variable property of a class or structure to indicate that the property’s initial value is calculated and stored at most once, when the property is first accessed. For an example of how to use the `lazy` attribute, see [Lazy Stored Properties](#).

`lazy`
> 通过将这个属性应用在一个类或者结构体的存储变量属性上，来指定这个属性的初始值只在第一次被读取时才进行一次计算。查看[懒惰存储属性](#)中给出的关于如何使用`lazy`的例子。

`noreturn`
> Apply this attribute to a function or method declaration to indicate that the corresponding type of that function or method, `T`, is `@noreturn T`. You can mark a function or method type with this attribute to indicate that the function or method doesn’t return to its caller.

> You can override a function or method that is not marked with the `noreturn` attribute with a function or method that is. That said, you can’t override a function or method that is marked with the `noreturn` attribute with a function or method that is not. Similar rules apply when you implement a protocol method in a conforming type.

`noreturn`
> 将这个属性应用在函数或者方法声明中来指定这个函数或者方法，`T`，是`@noreturn T`类型。你可以通过使用这个关键词来标记函数或者方法来表明这个函数或者方法不返回任何值给它的调用者。

> 你可以使用一个标记了这个属性的函数或者方法来覆盖一个没有标记过这个属性的函数或者方法，但是反过来不行。同样的，当你要实现一个协议方法时，也需要遵循这个规则。

`NSCopying`
> Apply this attribute to a stored variable property of a class. This attribute causes the property’s setter to be synthesized with a *copy* of the property’s value—returned by the `copyWithZone` method—instead of the value of the property itself. The type of the property must conform to the `NSCopying` protocol.

> The `NSCopying` attribute behaves in a way similar to the Objective-C `copy` property attribute.

`NSManaged`
> Apply this attribute to a stored variable property of a class that inherits from `NSManagedObject` to indicate that the storage and implementation of the property are provided dynamically by Core Data at runtime based on the associated entity description.

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
	
`optional`
> Apply this attribute to a protocol’s property, method, or subscript members to indicate that a conforming type isn’t required to implement those members.

> You can apply the `optional` attribute only to protocols that are marked with the `objc` attribute. As a result, only class types can adopt and conform to a protocol that contains optional member requirements. For more information about how to use the `optional` attribute and for guidance about how to access optional protocol members—for example, when you’re not sure whether a conforming type implements them—see [Optional Protocol Requirements](#).

`required`
> Apply this attribute to a designated or convenience initializer of a class to indicate that every subclass must implement that initializer.

> Required designated initializers must be implemented explicitly. Required convenience initializers can be either implemented explicitly or inherited when the subclass directly implements all of the superclass’s designated initializers (or when the subclass overrides the designated initializers with convenience initializers).

### Declaration Attributes Used by Interface Builder

Interface Builder attributes are declaration attributes used by Interface Builder to synchronize with Xcode. Swift provides the following Interface Builder attributes: `IBAction`, `IBDesignable`, `IBInspectable`, and `IBOutlet`. These attributes are conceptually the same as their Objective-C counterparts.

You apply the `IBOutlet` and `IBInspectable` attributes to property declarations of a class. You apply the `IBAction` attribute to method declarations of a class and the `IBDesignable` attribute to class declarations.

## Type Attributes

You can apply type attributes to types only. However, you can also apply the `noreturn` attribute to a function or method *declaration*.

`auto_closure`
> This attribute is used to delay the evaluation of an expression by automatically wrapping that expression in a closure with no arguments. Apply this attribute to a function or method type that takes no arguments and that returns the type of the expression. For an example of how to use the `auto_closure` attribute, see [Function Type](#).

`noreturn`
Apply this attribute to the type of a function or method to indicate that the function or method doesn’t return to its caller. You can also mark a function or method declaration with this attribute to indicate that the corresponding type of that function or method, `T`, is `@noreturn T`.

> GRAMMAR OF AN ATTRIBUTE

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


