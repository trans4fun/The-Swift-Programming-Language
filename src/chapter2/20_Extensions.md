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
- 将既有类型转换为符合某一个协议


Note
If you define an extension to add new functionality to an existing type, the new functionality will be available on all existing instances of that type, even if they were created before the extension was defined.

注意
