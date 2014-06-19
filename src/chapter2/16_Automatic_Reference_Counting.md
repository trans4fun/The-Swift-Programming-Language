# 自动引用计数

Swift uses Automatic Reference Counting (ARC) to track and manage your app’s memory usage. In most cases, this means that memory management “just works” in Swift, and you do not need to think about memory management yourself. ARC automatically frees up the memory used by class instances when those instances are no longer needed.

However, in a few cases ARC requires more information about the relationships between parts of your code in order to manage memory for you. This chapter describes those situations and shows how you enable ARC to manage all of your app’s memory.

Swift 使用自动引用计数（ARC）机制跟踪和管理APP的内存使用，大部分情况下，此机制是自动工作的，你没有必要考虑内存管理的事情。当一个类实例不再需要的时候，ARC会自动释放其占用的内存。

但少数情况下，ARC需要更多关于你代码之间的关系信息来帮你管理内存。本章介绍了这些情况，并向你示范如何启用ARC来管理你的APP的全部内存。

> NOTE
> 
> Reference counting only applies to instances of classes. Structures and enumerations are value types, not reference types, and are not stored and passed by reference.

> 注意
> 
> 引用计数仅适用于类实例。结构体和枚举类型是值类型而非引用类型, 也不是按照引用的方式存储和传递的，所以不适用引用计数机制。

## ARC是如何工作的
Every time you create a new instance of a class, ARC allocates a chunk of memory to store information about that instance. This memory holds information about the type of the instance, together with the values of any stored properties associated with that instance.

Additionally, when an instance is no longer needed, ARC frees up the memory used by that instance so that the memory can be used for other purposes instead. This ensures that class instances do not take up space in memory when they are no longer needed.

当你创建一个类实例的时候，ARC会为之分配一块内存来存储该实例的相关信息。这些信息包括：该实例的类型及其相关的属性和值。当该实例不再需要的时候，ARC会释放其占用的内存留作他用。这种机制保证了不需要的类实例占用的内存会及时得到释放。

However, if ARC were to deallocate an instance that was still in use, it would no longer be possible to access that instance’s properties, or call that instance’s methods. Indeed, if you tried to access the instance, your app would most likely crash.

To make sure that instances don’t disappear while they are still needed, ARC tracks how many properties, constants, and variables are currently referring to each class instance. ARC will not deallocate an instance as long as at least one active reference to that instance still exists.

然而，如果ARC释放了一个正在使用的类实例的内存，那会导致该实例的方法和属性都不能访问。而且，如果你试图访问已被ARC释放的实例，你的APP很可能会崩溃。

为了确保使用中的类实例不会无端消失（被ARC回收），ARC会跟踪和统计每个类实例被多少属性，常量，变量所引用。即使只有一个活动引用存在，该类实例也不会被ARC回收。

To make this possible, whenever you assign a class instance to a property, constant, or variable, that property, constant, or variable makes a strong reference to the instance. The reference is called a “strong“ reference because it keeps a firm hold on that instance, and does not allow it to be deallocated for as long as that strong reference remains.

为了保证ARC机制的有效运行，无论何时你将一个类实例分配给一个属性、常量或一个变量，那么这个属性、常量或变量与类实例之间将建立起一种强引用关系。之所以称为“强引用”，是它会牢牢保持与类实例的引用关系，只要指向类实例的强引用存在，该实例就是不允许被销毁的。

## ARC 实践
Here’s an example of how Automatic Reference Counting works. This example starts with a simple class called Person, which defines a stored constant property called name:

下面的例子展示了自动引用计数是如何工作的。这是一个名为Person的类，其内部定义了一个名为name的属性：

```
class Person {
    let name: String
    init(name: String) {
        self.name = name
        println("\(name) is being initialized")
    }
    deinit {
        println("\(name) is being deinitialized")
    }
}
```
The Person class has an initializer that sets the instance’s name property and prints a message to indicate that initialization is underway. The Person class also has a deinitializer that prints a message when an instance of the class is deallocated.


Person类有一个构造函数init，负责为其实例属性name赋值并打印出一条信息表明初始化过程正在进行。
Person类也有一个析构函数deinit，会在Person的实例被销毁时打印出一条信息。

The next code snippet defines three variables of type Person?, which are used to set up multiple references to a new Person instance in subsequent code snippets. Because these variables are of an optional type (Person?, not Person), they are automatically initialized with a value of nil, and do not currently reference a Person instance.

下面的代码片段定义了三个类型为Person?的变量，在随后的代码中，它们将用于设置指向一个Person类实例的多个引用。
由于这些变量是可选类型（类型为Person?，不是Person），他们将自动初始化为nil(即初始值为nil)，而不是引用到Person的实例。

```
var reference1: Person?
var reference2: Person?
var reference3: Person?
```

You can now create a new Person instance and assign it to one of these three variables:
现在你可以创建Person类的新实例，并且将它赋值给三个变量其中的一个：
```
reference1 = Person(name: "John Appleseed")
// prints "John Appleseed is being initialized”
```

Note that the message "John Appleseed is being initialized" is printed at the point that you call the Person class’s initializer. This confirms that initialization has taken place.

注意，当你调用Person类的构造函数的时候，此消息："John Appleseed is being initialized"将会被打印出来。这表明初始化已经完成。

Because the new Person instance has been assigned to the reference1 variable, there is now a strong reference from reference1 to the new Person instance. Because there is at least one strong reference, ARC makes sure that this Person is kept in memory and is not deallocated.

由于该Person实例被赋值给了变量reference1，因此建立了一个由reference1指向该Person实例的强引用。
ARC会保证该Person实例保持在内存中不被销毁，因为它这满足了至少有一个强引用的条件。

If you assign the same Person instance to two more variables, two more strong references to that instance are established:
如果你将该实例赋值给多个变量，那么就会建立指向该实例的多个强引用：
```
reference2 = reference1
reference3 = reference1
```
There are now three strong references to this single Person instance.
现在这个Person实例已经有三个强引用了。

If you break two of these strong references (including the original reference) by assigning nil to two of the variables, a single strong reference remains, and the Person instance is not deallocated:
如果你通过给任意两个变量赋值nil的方式断开两个强引用（包括原始引用），只留下一个强引用，该Person实例不会被销毁：
```
reference2 = nil
reference3 = nil
```
ARC does not deallocate the Person instance until the third and final strong reference is broken, at which point it is clear that you are no longer using the Person instance:
ARC不会销毁该Person实例，直到第三个也是最后一个强引用断开，即能够清楚的表明你不再需要该实例的时候。
```
reference3 = nil
// prints "John Appleseed is being deinitialized"
```

## 类实例间的强引用循环

In the examples above, ARC is able to track the number of references to the new Person instance you create and to deallocate that Person instance when it is no longer needed.

在上面的例子中，ARC能够跟踪指向Person实例的引用个数，并且在该Person实例不在需要的时候销毁它。

However, it is possible to write code in which an instance of a class never gets to a point where it has zero strong references. This can happen if two class instances hold a strong reference to each other, such that each instance keeps the other alive. This is known as a strong reference cycle.

然而，我们可能会写出这样的代码，导致一个类实例永远不会有0个强引用。这种情况发生在两个类实例互相保持对方的强引用，以致于彼此都无法被销毁。这就是所谓的强引用循环。

You resolve strong reference cycles by defining some of the relationships between classes as weak or unowned references instead of as strong references. This process is described in Resolving Strong Reference Cycles Between Class Instances. However, before you learn how to resolve a strong reference cycle, it is useful to understand how such a cycle is caused.
你可以通过定义类之间的关系为弱引用或者无主引用来替代强引用，从而解决循环强引用的问题。具体的过程在解决类实例之间的循环强引用中有描述。不管怎样，在你学习怎样解决循环强引用之前，很有必要了解一下它是如何产生的。

Here’s an example of how a strong reference cycle can be created by accident.
This example defines two classes called Person and Apartment, which model a block of apartments and its residents:
这是一个意外导致强引用循环的例子。例子定义了两个名为Person和Apartment的类，用来模拟公寓和公寓里的居民：
```
class Person {
    let name: String
    init(name: String) { self.name = name }
    var apartment: Apartment?
    deinit { println("\(name) is being deinitialized") }
}
 
class Apartment {
    let number: Int
    init(number: Int) { self.number = number }
    var tenant: Person?
    deinit { println("Apartment #\(number) is being deinitialized") }
}
```
Every Person instance has a name property of type String and an optional apartment property that is initially nil. The apartment property is optional, because a person may not always have an apartment.
每一个Person实例都有一个String类型的属性name和一个初始化为nil的可选类型属性apartment。之所以将apartment定义为可选类型，是因为某人可能不总是租公寓。

Similarly, every Apartment instance has a number property of type Int and has an optional tenant property that is initially nil. The tenant property is optional because an apartment may not always have a tenant.

类似的，每一个Apartment实例都有一个Int类型的属性number，和一个初始化为nil的可选类型属性tenant。之所以将tenant定义为可选类型，是因为某公寓也不总是有租客住。

Both of these classes also define a deinitializer, which prints the fact that an instance of that class is being deinitialized. This enables you to see whether instances of Person and Apartment are being deallocated as expected.

两个类都定义了析构函数，它们将在类实例被析构时输出一段信息。这能够让你清楚的知道Person和Apartment的实例是否如预期那样被销毁了。

This next code snippet defines two variables of optional type called john and number73, which will be set to a specific Apartment and Person instance below. Both of these variables have an initial value of nil, by virtue of being optional:

下面的代码片段定义了两个可选类型变量john和number73，接下来，他们将被设置为具体的Apartment实例和Person实例。两个变量的初始值都是nil，因为它们都是可选类型的：
```
var john: Person?
var number73: Apartment?
```
You can now create a specific Person instance and Apartment instance and assign these new instances to the john and number73 variables:
现在创建具体的Person实例和Apartment实例，并把这两个新实例分别赋值给john和number73：
```
john = Person(name: "John Appleseed")
number73 = Apartment(number: 73)
```
Here’s how the strong references look after creating and assigning these two instances. The john variable now has a strong reference to the new Person instance, and the number73 variable has a strong reference to the new Apartment instance:
下图展示了创建和分配两个实例之后的强引用关系。john变量和新Person实例之间有一条强引用关系，number73变量和新Apartment实例之间也有一条强引用关系。

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/referenceCycle01_2x.png)

