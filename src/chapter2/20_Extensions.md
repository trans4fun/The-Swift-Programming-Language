Extensions

Extensions add new functionality to an existing class, structure, or enumeration type. This includes the ability to extend types for which you do not have access to the original source code (known as retroactive modeling). Extensions are similar to categories in Objective-C. (Unlike Objective-C categories, Swift extensions do not have names.)
扩展为已有的类，结构，枚举添加新的功能。其中包括扩展没有访问权代码权限的类型（即追溯建模）。扩展和 Objective-C 当中的分类很相似。（与 Objective-C 中的分类不同的是，Swift 的扩展没有名字）


 Extensions in Swift can:
    Add computed properties and computed static properties
    Define instance methods and type methods
    Provide new initializers
    Define subscripts
    Define and use new nested types
    Make an existing type conform to a protocol

Swift 的扩展可以：
- 增加计算属性和静态计算属性
- 定义实例方法和类型方法
- 提供新的构造器
- 定义下标
- 定义和使用新的嵌套类型
- 将已有的类型转换为符合某一个协议


Note
If you define an extension to add new functionality to an existing type, the new functionality will be available on all existing instances of that type, even if they were created before the extension was defined.

注意
如果定义一个扩展用来在已有的类型上增加新的功能，那么新功能会应用在所有已经存在的实例上，即使是在扩展被定义之前实例化的。


Extension Syntax
Declare extensions with the extension keyword: 


扩展的语法
使用 extension 关键字来声明扩展

    extension SomeType {
        // new functionality to add to SomeType goes here
    }

An extension can extend an existing type to make it adopt one or more protocols. Where this is the case, the protocol names are written in exactly the same way as for a class or structure:
一个扩展可以扩展一个已有的类型，使它能适配一个或多个的协议。如果是这种情况的话，协议的命名方式应该与类和结构体的命名方式完全一致。

    extension SomeType: SomeProtocol, AnotherProtocol {
        // implementation of protocol requirements goes here
    }

Adding protocol conformance in this way is described in Adding Protocol Conformance with an Extension.
这种增加协议一致性的方式被称为通过扩展增加协议一致性


Computed Properties
计算属性

Extensions can add computed instance properties and computed type properties to existing types. This example adds five computed instance properties to Swift’s built-in Double type, to provide basic support for working with distance units: 
































