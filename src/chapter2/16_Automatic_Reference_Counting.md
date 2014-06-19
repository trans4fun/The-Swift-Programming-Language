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

现在创建Person类的新实例，并且将它赋值给三个变量中的一个：

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

如果你通过给任意两个变量赋值nil的方式断开两个强引用（包括原始引用），留下一个强引用，该Person实例不会被销毁：

```
reference2 = nil
reference3 = nil
```
ARC does not deallocate the Person instance until the third and final strong reference is broken, at which point it is clear that you are no longer using the Person instance:

直到第三个也是最后一个强引用断开，即能够清楚的断定你不再需要该实例的时候，ARC才会销毁该Person实例。

```
reference3 = nil
// prints "John Appleseed is being deinitialized"
```

## 类实例间的循环强引用

In the examples above, ARC is able to track the number of references to the new Person instance you create and to deallocate that Person instance when it is no longer needed.

在上面的例子中，ARC能够跟踪指向Person实例的引用个数，并且在该Person实例不再需要的时候销毁它。

However, it is possible to write code in which an instance of a class never gets to a point where it has zero strong references. This can happen if two class instances hold a strong reference to each other, such that each instance keeps the other alive. This is known as a strong reference cycle.

然而，我们可能会写出这样的代码，导致类实例永远不会有0个强引用。这种情况发生在两个类实例互相保持对方的强引用，以致于彼此都无法被销毁的时候。这就是所谓的循环强引用。

You resolve strong reference cycles by defining some of the relationships between classes as weak or unowned references instead of as strong references. This process is described in Resolving Strong Reference Cycles Between Class Instances. However, before you learn how to resolve a strong reference cycle, it is useful to understand how such a cycle is caused.

你可以通过定义类之间的关系为弱引用或者无主引用的方式来解决循环强引用的问题。具体的过程在解决类实例之间的循环强引用中有描述。不管怎样，在你学习怎样解决循环强引用之前，很有必要了解一下它是如何产生的。

Here’s an example of how a strong reference cycle can be created by accident.
This example defines two classes called Person and Apartment, which model a block of apartments and its residents:

这是一个意外导致循环强引用的例子。例子定义了两个名为Person和Apartment的类，用来模拟公寓和公寓里的居民：

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

这里展示了创建和分配两个实例之后的强引用关系。john变量和新Person实例之间有一条强引用关系，number73变量和新Apartment实例之间也有一条强引用关系。

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/referenceCycle01_2x.png)

You can now link the two instances together so that the person has an apartment, and the apartment has a tenant. Note that an exclamation mark (!) is used to unwrap and access the instances stored inside the john and number73 optional variables, so that the properties of those instances can be set:

现在将两个实例连接在一起，让人住进一间公寓，公寓也有了一个租客。注意那个感叹号（!），它用于打开和访问存储于john和number73实例中的可选变量，这样实例的属性才能够被设置：

```
john!.apartment = number73
number73!.tenant = john
```

Here’s how the strong references look after you link the two instances together:
这里展示了两个实例连接在一起之后的强引用关系：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/referenceCycle02_2x.png)

Unfortunately, linking these two instances creates a strong reference cycle between them. The Person instance now has a strong reference to the Apartment instance, and the Apartment instance has a strong reference to the Person instance. Therefore, when you break the strong references held by the john and number73 variables, the reference counts do not drop to zero, and the instances are not deallocated by ARC:

不幸的是，连接两个实例后导致它们之间形成了循环强引用。现在Person实例有一个指向Apartment的强引用，同时Apartment实例也有一个指向Person的强引用。因此，当你断开由变量john和number73保持的强引用时，引用计数不会减为0，因此实例也不会被ARC销毁。

```
john = nil
number73 = nil
```

Note that neither deinitializer was called when you set these two variables to nil. The strong reference cycle prevents the Person and Apartment instances from ever being deallocated, causing a memory leak in your app.

需要注意的是，你将john和number73设为nil时两个析构函数都没有被调用。循环强引用阻止了Person 和 Apartment类实例的销毁，在你的App中导致了内存泄漏。

Here’s how the strong references look after you set the john and number73 variables to nil:

下图展示了将john和number73设为nil后的强引用关系：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/referenceCycle03_2x.png)

The strong references between the Person instance and the Apartment instance remain and cannot be broken.

Person类实例与Apartment类实例之间的强引用关系将保持且无法被断开。

## 解决类实例间的循环强引用

Swift provides two ways to resolve strong reference cycles when you work with properties of class type: weak references and unowned references.

Swift提供了两种方式来解决你在处理类属性时遇到的循环强引用问题：弱引用和无主引用。

Weak and unowned references enable one instance in a reference cycle to refer to the other instance without keeping a strong hold on it. The instances can then refer to each other without creating a strong reference cycle.

弱引用和无主引用允许循环引用中的一个实例引用另外一个实例而不保持强引用。这样实例能够互相引用而不产生循环强引用。

Use a weak reference whenever it is valid for that reference to become nil at some point during its lifetime. Conversely, use an unowned reference when you know that the reference will never be nil once it has been set during initialization.

对于生命周期中会变为nil的实例使用弱引用。相反的，对于初始化赋值后再也不会被赋值为nil的实例，使用无主引用。

### 弱引用

A weak reference is a reference that does not keep a strong hold on the instance it refers to, and so does not stop ARC from disposing of the referenced instance. This behavior prevents the reference from becoming part of a strong reference cycle. You indicate a weak reference by placing the weak keyword before a property or variable declaration.

弱引用不会强制保持引用的实例，并且不会阻止 ARC 销毁被引用的实例。这阻止了引用成为循环强引用的组成部分。声明属性或者变量时，在前面加上weak关键字表明这是一个弱引用。

Use a weak reference to avoid reference cycles whenever it is possible for that reference to have “no value” at some point in its life. If the reference will always have a value, use an unowned reference instead, as described in Unowned References. In the Apartment example above, it is appropriate for an apartment to be able to have “no tenant” at some point in its lifetime, and so a weak reference is an appropriate way to break the reference cycle in this case.

在引用对象的生命周期中，如果某些时候引用对象可能无值，就使用弱引用阻止产生循环强引用。如果引用对象总是有值，则应使用无主引用，这将在无主引用部分详述。在上面Apartment的例子中，一个公寓的生命周期中，有时是没有“租客”的，这种情况下适合使用弱引用来打破引用循环。

> NOTE
> 
> Weak references must be declared as variables, to indicate that their value can change at runtime. A weak reference cannot be declared as a constant.
> 注意
> 弱引用必须声明为变量，以表明它们的值在运行时是可以改变的。弱引用不能声明为常量。

Because weak references are allowed to have “no value”, you must declare every weak reference as having an optional type. Optional types are the preferred way to represent the possibility for “no value” in Swift.

由于弱引用类型允许没有值，因此你必须声明所有弱引用变量为可选类型。在Swift里，可选类型是表示可能没有值的变量的首选方式。

Because a weak reference does not keep a strong hold on the instance it refers to, it is possible for that instance to be deallocated while the weak reference is still referring to it. Therefore, ARC automatically sets a weak reference to nil when the instance that it refers to is deallocated. You can check for the existence of a value in the weak reference, just like any other optional value, and you will never end up with a reference to an invalid instance that no longer exists.

由于弱引用与其指向的实例之间不会保持强引用关系，因此即使有弱引用指向实例，实例也有可能被销毁。弱引用指向的实例被销毁后，ARC会将该弱引用指向nil。像其他可选类型变量一样，你可以检查弱引用类型的变量是否存在值来避免引用一个不存在的实例。

The example below is identical to the Person and Apartment example from above, with one important difference. This time around, the Apartment type’s tenant property is declared as a weak reference:

下面的例子与上文提到的Person 和 Apartment 的例子类似，但有一处重要的不同。这次，Apartment的属性tenant被声明为弱引用类型：

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
    weak var tenant: Person?
    deinit { println("Apartment #\(number) is being deinitialized") }
}
```
The strong references from the two variables (john and number73) and the links between the two instances are created as before:

两个变量（john和number73）的强引用以及两个实例之间的连接都与之前一样被创建：

```
var john: Person?
var number73: Apartment?

john = Person(name: "John Appleseed")
number73 = Apartment(number: 73)

john!.apartment = number73
number73!.tenant = john
```

Here’s how the references look now that you’ve linked the two instances together:
下图展示了现在的引用关系：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/weakReference01_2x.png)

The Person instance still has a strong reference to the Apartment instance, but the Apartment instance now has a weak reference to the Person instance. This means that when you break the strong reference held by the john variables, there are no more strong references to the Person instance:

Person实例依然保持对Apartment实例的强引用，但是Apartment实例只有对Person实例的弱引用。这意味着当你断开john变量所保持的强引用时，就没有指向Person实例的强引用了：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/weakReference02_2x.png)

Because there are no more strong references to the Person instance, it is deallocated:
由于没有指向Person实例的强引用了，所以它被销毁了：

```
john = nil
// prints "John Appleseed is being deinitialized"
```
The only remaining strong reference to the Apartment instance is from the number73 variable. If you break that strong reference, there are no more strong references to the Apartment instance:

仅存的指向Apartment实例的强引用来自变量number73。如果你断开这个强引用，也就没有强引用指向Apartment的实例了：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/weakReference03_2x.png)

Because there are no more strong references to the Apartment instance, it too is deallocated:
由于也没有指向Apartment类实例的强引用了，它也被销毁了：

```
number73 = nil
// prints "Apartment #73 is being deinitialized"
```

The final two code snippets above show that the deinitializers for the Person instance and Apartment instance print their “deinitialized” messages after the john and number73 variables are set to nil. This proves that the reference cycle has been broken.

上面的两段代码展示了变量john和number73在被赋值为nil后，Person实例和Apartment实例的析构函数都打印出“销毁”的信息。这证明了引用循环被打破了。

### 无主引用

Like weak references, an unowned reference does not keep a strong hold on the instance it refers to. Unlike a weak reference, however, an unowned reference is assumed to always have a value. Because of this, an unowned reference is always defined as a non-optional type. You indicate an unowned reference by placing the unowned keyword before a property or variable declaration.

与弱引用类似，无主引用也不会与其指向的类实例间保持强引用关系。不同的是，无主引用假定一直都是有值的。因此，无主引用总是被定义为非可选类型。你可以在属性和变量之前加上unowned关键词来声明这是无主引用。

Because an unowned reference is non-optional, you don’t need to unwrap the unowned reference each time it is used. An unowned reference can always be accessed directly. However, ARC cannot set the reference to nil when the instance it refers to is deallocated, because variables of a non-optional type cannot be set to nil.

由于无主引用是非可选类型的，你不必在使用的时候展开它，它可以被直接访问。与弱引用不同，当无主引用指向的实例被销毁后，ARC不会将其指向nil。

> NOTE
> 
> If you try to access an unowned reference after the instance that it references is deallocated, you will trigger a runtime error. Use unowned references only when you are sure that the reference will always refer to an instance.
> 
> Note also that Swift guarantees your app will crash if you try to access an unowned reference after the instance it references is deallocated. You will never encounter unexpected behavior in this situation. Your app will always crash reliably, although you should, of course, prevent it from doing so.
> 注意
> 在无主引用指向的实例被销毁后，如果依然试图访问该无主引用，你会触发运行时错误。使用无主引用，需要你你能够确保引用指向的实例未被销毁。
> 需要格外注意的是，在无主引用指向的实例被销毁后，你依然试图访问该无主引用，Swift保证，你的app会毫无意外地直接崩溃，这确实会发生。不是应该而是你必须阻止这样的情况发生。