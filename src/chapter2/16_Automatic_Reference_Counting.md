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

然而，如果ARC释放了一个正在使用的类实例的内存，那会导致该实例的方法和属性都不能访问。而且，如果你试图访问已被ARC释放的实例，你的APP多半会崩溃。

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

你可以通过定义类之间的关系为弱引用或者无主引用的方式来解决循环强引用的问题。具体过程将在“解决类实例之间的循环强引用”中详述。不管怎样，在学习怎样解决循环强引用之前，很有必要了解一下它是如何产生的。

Here’s an example of how a strong reference cycle can be created by accident.
This example defines two classes called Person and Apartment, which model a block of apartments and its residents:

这是一个意外导致循环强引用的例子。例子定义了名为Person和Apartment的两个类，用来模拟公寓和公寓里的居民：

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

现在将两个实例连接在一起，让john住进number73公寓，number73公寓也有了一个租客john。注意那个感叹号（!），它用于解析和访问存储于john和number73实例中的可选变量，这样实例的属性才能够被设置：

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

需要注意的是，你将john和number73设为nil时两个析构函数都没有被调用。循环强引用阻止了Person 和 Apartment类实例的销毁，这在你的App中导致了内存泄漏。

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

弱引用不会强制保持引用的实例，并且不会阻止 ARC 销毁被引用的实例。这避免了引用成为循环强引用的组成部分。声明属性或者变量时，在前面加上weak关键字表明这是一个弱引用。

Use a weak reference to avoid reference cycles whenever it is possible for that reference to have “no value” at some point in its life. If the reference will always have a value, use an unowned reference instead, as described in Unowned References. In the Apartment example above, it is appropriate for an apartment to be able to have “no tenant” at some point in its lifetime, and so a weak reference is an appropriate way to break the reference cycle in this case.

在引用的生命周期中，如果某些时候引用可能无值，就使用弱引用避免产生循环强引用。如果引用总是有值，则应使用无主引用，这将在无主引用部分详述。在上面Apartment的例子中，一个公寓的生命周期中，有时是没有“租客”的，这种情况下适合使用弱引用来打破引用循环。

> NOTE
> 
> Weak references must be declared as variables, to indicate that their value can change at runtime. A weak reference cannot be declared as a constant.
> 注意
> 弱引用必须声明为变量而不能声明为常量，以表明它们的值在运行时是可以改变的。

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

由于无主引用是非可选类型的，你不必在使用的时候解析它，它可以被直接访问。与弱引用不同，当无主引用指向的实例被销毁后，ARC不会将其指向nil。

> NOTE
> 
> If you try to access an unowned reference after the instance that it references is deallocated, you will trigger a runtime error. Use unowned references only when you are sure that the reference will always refer to an instance.
> 
> Note also that Swift guarantees your app will crash if you try to access an unowned reference after the instance it references is deallocated. You will never encounter unexpected behavior in this situation. Your app will always crash reliably, although you should, of course, prevent it from doing so.

> 注意
> 在无主引用指向的实例被销毁后，如果依然试图访问该无主引用，你会触发运行时错误。使用无主引用，需要你你能够确保引用指向的实例未被销毁。
> 需要格外注意的是，在无主引用指向的实例被销毁后，若你依然试图访问该无主引用，Swift保证，你的app会毫无意外地直接崩溃。不是应该而是你必须避免这样的情况发生。

The following example defines two classes, Customer and CreditCard, which model a bank customer and a possible credit card for that customer. These two classes each store an instance of the other class as a property. This relationship has the potential to create a strong reference cycle.

接下来的例子定义了两个类，Customer和CreditCard，分别为银行客户和信用卡建模。这两个类通过属性互相保存了对方的实例。这种关系，在它们之间潜在地形成了循环强引用。

The relationship between Customer and CreditCard is slightly different from the relationship between Apartment and Person seen in the weak reference example above. In this data model, a customer may or may not have a credit card, but a credit card will always be associated with a customer. To represent this, the Customer class has an optional card property, but the CreditCard class has a non-optional customer property.

Customer 与 CreditCard之间的关系与上文弱引用例子里提到的Apartment 和 Person之间的关系有些许不同。在这个数据模型里，一位客户可能有也可能没有信用卡，但是一张信用卡必然与某位银行客户关联。为了表示这种关系，Customer类声明了一个可选类型的属性card，但CreditCard类声明了一个非可选类型的属性customer。

Furthermore, a new CreditCard instance can only be created by passing a number value and a customer instance to a custom CreditCard initializer. This ensures that a CreditCard instance always has a customer instance associated with it when the CreditCard instance is created.

此外，只能通过向CreditCard类构造器传递一个数值和一个Customer类实例的方式创建新的CreditCard类实例。这是为了保证创建CreditCard类实例的时候总是有一位客户实例与之关联。

Because a credit card will always have a customer, you define its customer property as an unowned reference, to avoid a strong reference cycle:

由于一张信用卡一定会有一位客户实例与之关联，你将其属性customer定义为无主类型以避免循环强引用：

```
class Customer {
    let name: String
    var card: CreditCard?
    init(name: String) {
        self.name = name
    }
    deinit { println("\(name) is being deinitialized") }
}
 
class CreditCard {
    let number: Int
    unowned let customer: Customer
    init(number: Int, customer: Customer) {
        self.number = number
        self.customer = customer
    }
    deinit { println("Card #\(number) is being deinitialized") }
}
```

This next code snippet defines an optional Customer variable called john, which will be used to store a reference to a specific customer. This variable has an initial value of nil, by virtue of being optional:

如下代码片段定义了一个可选Customer类型的变量john，john将用于存储到特定客户的引用。由于是可选类型，这个变量初始值是nil.

```
var john: Customer?
```

You can now create a Customer instance, and use it to initialize and assign a new CreditCard instance as that customer’s card property:

现在创建Customer类实例，并用它初始化CreditCard类实例，同时，将CreditCard类实例分配给Customer类实例的客户属性。

```
john = Customer(name: "John Appleseed")
john!.card = CreditCard(number: 1234_5678_9012_3456, customer: john!)
```

Here’s how the references look, now that you’ve linked the two instances:

下图展示了两个实例连接起来后的引用关系：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/unownedReference01_2x.png)

The Customer instance now has a strong reference to the CreditCard instance, and the CreditCard instance has an unowned reference to the Customer instance.

Customer类实例拥有一个指向CreditCard类实例的强引用，同时CreditCard类实例有一个指向Customer类实例的无主引用。

Because of the unowned customer reference, when you break the strong reference held by the john variable, there are no more strong references to the Customer instance:

由于无主引用customer的存在，当你断开由变量john保持的强引用后，就没有强引用指向Customer类实例了：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/unownedReference02_2x.png)

Because there are no more strong references to the Customer instance, it is deallocated. After this happens, there are no more strong references to the CreditCard instance, and it too is deallocated:

由于没有强引用指向Customer类实例了，它被销毁了。在此之后，由于也没有强引用指向CreditCard类实例了，它也被销毁了。

```
john = nil
// prints "John Appleseed is being deinitialized"
// prints "Card #1234567890123456 is being deinitialized"
```

The final code snippet above shows that the deinitializers for the Customer instance and CreditCard instance both print their “deinitialized” messages after the john variable is set to nil.

上面的代码展示了变量john被赋值为nil后，Customer实例和CreditCard实例的析构函数都打印出了“销毁”的信息。

## 无主引用与隐式解析可选属性

The examples for weak and unowned references above cover two of the more common scenarios in which it is necessary to break a strong reference cycle.

弱引用和无主引用的例子涵盖了两种常用的需要打破循环强引用的场景。

The Person and Apartment example shows a situation where two properties, both of which are allowed to be nil, have the potential to cause a strong reference cycle. This scenario is best resolved with a weak reference.

Person和Apartment的例子展示了两个属性的值都允许为nil，并会潜在地产生循环强引用。这种场景最适合用弱引用来解决。

The Customer and CreditCard example shows a situation where one property that is allowed to be nil and another property that cannot be nil have the potential to cause a strong reference cycle. This scenario is best resolved with an unowned reference.

Customer和CreditCard的例子展示了一个属性的值允许为nil，而另一个不允许为nil，并会潜在地产生循环强引用。这种场景最适合通过无主引用来解决。

However, there is a third scenario, in which both properties should always have a value, and neither property should ever be nil once initialization is complete. In this scenario, it is useful to combine an unowned property on one class with an implicitly unwrapped optional property on the other class.

但是，还有第三种场景：就是两个属性都一直有值，并且一旦初始化完成他们就永远都不可能是nil的情况。这种情况下，在一个类中使用无主属性，在另一个类中使用隐式解析可选属性，是解决此类循环强引用问题的有效手段。

This enables both properties to be accessed directly (without optional unwrapping) once initialization is complete, while still avoiding a reference cycle. This section shows you how to set up such a relationship.

只要初始化完成，这两个属性都是可以被直接访问的（没有可选类型的解析过程）同时也可以避免循环引用。这部分将向你介绍如何建立这种关系。

The example below defines two classes, Country and City, each of which stores an instance of the other class as a property. In this data model, every country must always have a capital city, and every city must always belong to a country. To represent this, the Country class has a capitalCity property, and the City class has a country property:

下面的例子定义了两个类，Country 和 City，它们彼此通过属性保存了对方的实例引用。在这个数据模型里，国家是必须有首都的，而一个城市也必须是属于某个国家。为了表示这种关系，Country类声明了一个capitalCity属性，City类也声明了一个country属性：

```
class Country {
    let name: String
    let capitalCity: City!
    init(name: String, capitalName: String) {
        self.name = name
        self.capitalCity = City(name: capitalName, country: self)
    }
}
 
class City {
    let name: String
    unowned let country: Country
    init(name: String, country: Country) {
        self.name = name
        self.country = country
    }
}
```

To set up the interdependency between the two classes, the initializer for City takes a Country instance, and stores this instance in its country property.

为了构建两个类之间的依赖关系，City类的构造器接收一个Country实例并把它存储在country属性里。

The initializer for City is called from within the initializer for Country. However, the initializer for Country cannot pass self to the City initializer until a new Country instance is fully initialized, as described in Two-Phase Initialization.

City的构造器将在Country的构造器里被调用。但是，Country的构造器无法传递自身（`self`）到City的构造器，直到Country实例已完全初始化。这在[两段式构造过程](http://TODO)中有介绍。

To cope with this requirement, you declare the capitalCity property of Country as an implicitly unwrapped optional property, indicated by the exclamation mark at the end of its type annotation (City!). This means that the capitalCity property has a default value of nil, like any other optional, but can be accessed without the need to unwrap its value as described in Implicitly Unwrapped Optionals.

为了满足要求，你将Country类的capitalCity属性声明为隐式解析可选属性（通过在capitalCity类型后加感叹号`City!`来声明）。这意味着，像其他可选类型属性一样，capitalCity属性的默认值为nil, 但是它可以不经解析直接被访问。这在[隐式解析可选类型](http://TODO)中有详细介绍。

Because capitalCity has a default nil value, a new Country instance is considered fully initialized as soon as the Country instance sets its name property within its initializer. This means that the Country initializer can start to reference and pass around the implicit self property as soon as the name property is set. The Country initializer can therefore pass self as one of the parameters for the City initializer when the Country initializer is setting its own capitalCity property.

由于capitalCity默认值为nil, 因此当Country实例的name属性在构造器内被赋值的时候，就认为初始化已经全部完成。这意味着name属性一被赋值，Country类构造器就可以开始引用和传递隐式的`self`。Country构造器也因此可以在为capitalCity属性赋值时把`self`作为参数给City的构造器。

All of this means that you can create the Country and City instances in a single statement, without creating a strong reference cycle, and the capitalCity property can be accessed directly, without needing to use an exclamation mark to unwrap its optional value:

上述这一切，意味着你可以在单一语句中同时创建Country和City的实例，这里没有形成循环强引用，同时capitalCity也可以直接被访问，也不必用感叹号来解析其可选值，如下所示：

```
var country = Country(name: "Canada", capitalName: "Ottawa")
println("\(country.name)'s capital city is called \(country.capitalCity.name)")
// prints "Canada's capital city is called Ottawa
```

In the example above, the use of an implicitly unwrapped optional means that all of the two-phase class initializer requirements are satisfied. The capitalCity property can be used and accessed like a non-optional value once initialization is complete, while still avoiding a strong reference cycle.

在上面的例子中，应用“隐式解析可选属性”使得两段式类构造器所需要的条件均得到满足。一旦初始化完成，capitalCity属性可以像非可选值那样被直接访问，同时还避免了循环强引用。

## 闭包引起的循环强引用
You saw above how a strong reference cycle can be created when two class instance properties hold a strong reference to each other. You also saw how to use weak and unowned references to break these strong reference cycles.

在上文中你已经了解了两个实例属性互相保持彼此的强引用是如何导致循环强引用的。你也知道了可以利用弱引用和无主引用来断开强引用循环。

A strong reference cycle can also occur if you assign a closure to a property of a class instance, and the body of that closure captures the instance. This capture might occur because the closure’s body accesses a property of the instance, such as self.someProperty, or because the closure calls a method on the instance, such as self.someMethod(). In either case, these accesses cause the closure to “capture” self, creating a strong reference cycle.

如果你将一个闭包分配给一个类实例的属性，同时闭包内部又捕获了该实例，也会形成循环强引用。这种捕获之所以可能发生，是因为闭包内部访问了该实例的属性，如：self.someProperty，或是访问了该实例的方法，如：self.someMethod()。这两种类型的访问，都会导致闭包“捕获”self，造成循环强引用。

This strong reference cycle occurs because closures, like classes, are reference types. When you assign a closure to a property, you are assigning a reference to that closure. In essence, it’s the same problem as above—two strong references are keeping each other alive. However, rather than two class instances, this time it’s a class instance and a closure that are keeping each other alive.

这种因闭包导致的循环强引用，和“类”的情况类似，都是引用类型的问题。

Swift provides an elegant solution to this problem, known as a closure capture list. However, before you learn how to break a strong reference cycle with a closure capture list, it is useful to understand how such a cycle can be caused.

针对这类问题，Swift提供了一种优雅的解决方案：闭包捕获列表。

The example below shows how you can create a strong reference cycle when using a closure that references self. This example defines a class called HTMLElement, which provides a simple model for an individual element within an HTML document:

下面的例子展示了闭包是如何导致循环强引用的。例子定义了一个名为HTMLElement的类，为HTML文档中的一类元素建模：

```
class HTMLElement {
    
    let name: String
    let text: String?
    
    @lazy var asHTML: () -> String = {
        if let text = self.text {
            return "<\(self.name)>\(text)</\(self.name)>"
        } else {
            return "<\(self.name) />"
        }
    }
    
    init(name: String, text: String? = nil) {
        self.name = name
        self.text = text
    }
    
    deinit {
        println("\(name) is being deinitialized")
    }
    
}
```

The HTMLElement class defines a name property, which indicates the name of the element, such as "p" for a paragraph element, or "br" for a line break element. HTMLElement also defines an optional text property, which you can set to a string that represents the text to be rendered within that HTML element.

HTMLElement类定义了一个name属性，用于标明元素的名称，如：“p”是段落元素的名称，或“br”是换行元素的名称。同时定义了一个可选类型的text属性，用于设置元素内需要渲染的内容。

In addition to these two simple properties, the HTMLElement class defines a lazy property called asHTML. This property references a closure that combines name and text into an HTML string fragment. The asHTML property is of type () -> String, or “a function that takes no parameters, and returns a String “value”.

除了这两个普通的属性之外，HTMLElement类还定义了一个懒属性asHTML。这个属性引用了一个用于将name和text合并为HTML片段的闭包。asHTML属性的类型是 `() -> String` 或描述为“一个返回字符串的无参函数”。

By default, the asHTML property is assigned a closure that returns a string representation of an HTML tag. This tag contains the optional text value if it exists, or no text content if text does not exist. For a paragraph element, the closure would return "&lt;p&gt;some text&lt;/p&gt;" or "&lt;p /&gt;", depending on whether the text property equals "some text" or nil.

默认情况下，asHTML属性被分配了一个闭包，这个闭包返回一个字符串形式的HTML标签。如果text的值存在就返回包含text值的标签，如果text的值不存在就返回不包含text值的标签。比如：一个段落标签，闭包会返回"&lt;p&gt;some text&lt;/p&gt;" 或 "&lt;p /&gt;"，这取决于text属性的值是"some text"还是nil。

The asHTML property is named and used somewhat like an instance method. However, because asHTML is a closure property rather than an instance method, you can replace the default value of the asHTML property with a custom closure, if you want to change the HTML rendering for a particular HTML element.

尽管asHTML是命名属性且用法类似实例方法，但是，由于asHTML是闭包属性而不是实例方法，因此如果你想渲染一个特定的HTML元素你可以用自定义闭包替换asHTML属性的默认值。

> 
> NOTE
> 
> The asHTML property is declared as a lazy property, because it is only needed if and when the element actually needs to be rendered as a string value for some HTML output target. The fact that asHTML is a lazy property means that you can refer to self within the default closure, because the lazy property will not be accessed until after initialization has been completed and self is known to exist.
> 注意
> asHTML之所以被声明为懒属性，是为了满足某些HTML输出需要，并且该元素确实需要渲染为字符串的情况下才被调用。事实上，声明asHTML为懒属性是为了在默认闭包内部引用self，因为懒属性只有在初始化完成且self已存在的情况下才能被访问。

The HTMLElement class provides a single initializer, which takes a name argument and (if desired) a text argument to initialize a new element. The class also defines a deinitializer, which prints a message to show when an HTMLElement instance is deallocated.

HTMLElement类提供了单一的构造器，它需要传递两个参数来初始化一个新元素：name（若需要） 和 text。同时定义了析构函数，当HTMLElement的实例被销毁的时候会打印出一条提示信息。

Here’s how you use the HTMLElement class to create and print a new instance:

这里展示了如何创建和打印HTMLElement类的新实例：

```
var paragraph: HTMLElement? = HTMLElement(name: "p", text: "hello, world")
println(paragraph!.asHTML())
// prints "<p>hello, world</p>
```
> 
> NOTE
> 
> The paragraph variable above is defined as an optional HTMLElement, so that it can be set to nil below to demonstrate the presence of a strong reference cycle.
> 注意
> 上面的paragraph变量被定义为可选类型是为了便于接下来可以设置为nil演示循环强引用。

Unfortunately, the HTMLElement class, as written above, creates a strong reference cycle between an HTMLElement instance and the closure used for its default asHTML value. Here’s how the cycle looks:

不幸的是，上面的HTMLElement类，在其类实例和做为asHTML默认值的闭包之间形成了循环强引用，如下所示：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/closureReferenceCycle01_2x.png)

The instance’s asHTML property holds a strong reference to its closure. However, because the closure refers to self within its body (as a way to reference self.name and self.text), the closure captures self, which means that it holds a strong reference back to the HTMLElement instance. A strong reference cycle is created between the two. (For more information about capturing values in a closure, see Capturing Values.)

实例的asHTML属性保持了一个指向它闭包的强引用。由于在闭包内部引用了self（作为访问self.name和self.text的途径），闭包捕获了self, 这意味着闭包也保持了指回HTMLElement的强引用。二者之间形成了循环强引用。（了解更多关于闭包值捕获有关的信息，请查看[值捕获](HTMLElement)有关的内容）

> NOTE
> 
> Even though the closure refers to self multiple times, it only captures one strong reference to the HTMLElement instance.
> 注意
> 尽管闭包引用了self多次，但只会捕获一个指向HTMLElement实例的强引用。

If you set the paragraph variable to nil and break its strong reference to the HTMLElement instance, neither the HTMLElement instance nor its closure are deallocated, because of the strong reference cycle:

即使将paragraph变量设置为nil来断开其与HTMLElement实例间的强引用，HTMLElement实例与其闭包也不会被销毁，因为它们之间存在循环强引用：

> paragraph = nil

Note that the message in the HTMLElement deinitializer is not printed, which shows that the HTMLElement instance is not deallocated.

注意到HTMLElement析构函数的信息并没有打印出来，这说明HTMLElement实例并未被销毁。

## 解决闭包引起的循环强引用
You resolve a strong reference cycle between a closure and a class instance by defining a capture list as part of the closure’s definition. A capture list defines the rules to use when capturing one or more reference types within the closure’s body. As with strong reference cycles between two class instances, you declare each captured reference to be a weak or unowned reference rather than a strong reference. The appropriate choice of weak or unowned depends on the relationships between the different parts of your code.

你可以在闭包的定义内附加定义捕获列表来解决闭包和类实例间的循环强引用问题。捕获列表为在闭包内使用一个或多个引用类型定义了一套规则。与解决两个类实例之间形成循环强引用方式一样，你应声明每个捕获的引用为弱类型或无主类型，而不是强引用类型。到底选择那种类型要看你代码不同部分之间的关系。

> NOTE
> 
> Swift requires you to write self.someProperty or self.someMethod (rather than just someProperty or someMethod) whenever you refer to a member of self within a closure. This helps you remember that it’s possible to capture self by accident.
> 注意
> 在闭包内引用self成员时，Swift要求以self.someProperty或self.someMethod的方式来引用，而不是以直接使用属性或方法名的方式引用（如：someProperty 或 someMethod）。这帮你记得闭包内引用self可能意外导致self被捕获。

### 定义捕获列表
Each item in a capture list is a pairing of the weak or unowned keyword with a reference to a class instance (such as self or someInstance). These pairings are written within a pair of square braces, separated by commas.

捕获列表的每一项都是weak或unown关键字和需引用的类实例（如：self或someInstance）成对组成。每一对由方括号包裹，以逗号分隔。


Place the capture list before a closure’s parameter list and return type if they are provided:

将捕获列表放在闭包参数列表和返回类型声明（若有返回值）之前：

```
@lazy var someClosure: (Int, String) -> String = {
    [unowned self] (index: Int, stringToProcess: String) -> String in
    // closure body goes here
}
```

If a closure does not specify a parameter list or return type because they can be inferred from context, place the capture list at the very start of the closure, followed by the in keyword:

若闭包没有确切的参数列表或返回类型（因为参数或返回类型可通过上下文推断），请将捕获列表放在闭包的最前面，并在后面加上in关键字。

```
@lazy var someClosure: () -> String = {
    [unowned self] in
    // closure body goes here
}
```

### 弱引用与无主引用
Define a capture in a closure as an unowned reference when the closure and the instance it captures will always refer to each other, and will always be deallocated at the same time.

当闭包和它捕获的实例总是互相引用且同时被销毁的时候，将闭包内的捕获定义为无主引用。

Conversely, define a capture as a weak reference when the captured reference may become nil at some point in the future. Weak references are always of an optional type, and automatically become nil when the instance they reference is deallocated. This enables you to check for their existence within the closure’s body.

相反的，如果捕获的实例在将来的某一时刻会变为nil，就将捕获定义为弱引用。弱引用总是可选类型，而且如果它们引用的实例被销毁了，它们会自动变为nil。因此可以很容易的在闭包内检查他们是否存在。

> NOTE
> 
> If the captured reference will never become nil, it should always be captured as an unowned reference, rather than a weak reference.
> 注意
> 如果捕获的引用永远不会变为nil,就要将该捕获定义为无主引用，而不是弱引用。

An unowned reference is the appropriate capture method to use to resolve the strong reference cycle in the HTMLElement example from earlier. Here’s how you write the HTMLElement class to avoid the cycle:

根据上述的判断原则，无主引用就是解决先前HTMLElement例子里循环强引用问题的合适方式。
这是改写后的HTMLElement类，避免了引用循环：

```
class HTMLElement {
    
    let name: String
    let text: String?
    
    @lazy var asHTML: () -> String = {
        [unowned self] in
        if let text = self.text {
            return "<\(self.name)>\(text)</\(self.name)>"
        } else {
            return "<\(self.name) />"
        }
    }
    
    init(name: String, text: String? = nil) {
        self.name = name
        self.text = text
    }
    
    deinit {
        println("\(name) is being deinitialized")
    }
    
}
```

This implementation of HTMLElement is identical to the previous implementation, apart from the addition of a capture list within the asHTML closure. In this case, the capture list is [unowned self], which means “capture self as an unowned reference rather than a strong reference”.

这次HTMLElement类的实现与之前的一样，除了在asHTML闭包内增加了一个捕获列表。在这个例子里，捕获列表是[unowned self]，意思是：“用无主引用而不是强引用来捕获self”

You can create and print an HTMLElement instance as before:
你依然可以想之前那样创建并打印HTMLElement实例：

```
var paragraph: HTMLElement? = HTMLElement(name: "p", text: "hello, world")
println(paragraph!.asHTML())
// prints "&lt;p&gt;hello, world&lt;/p&gt;"
```

Here’s how the references look with the capture list in place:

这是使用了捕获列表后的引用关系：

![](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/closureReferenceCycle02_2x.png)


This time, the capture of self by the closure is an unowned reference, and does not keep a strong hold on the HTMLElement instance it has captured. If you set the strong reference from the paragraph variable to nil, the HTMLElement instance is deallocated, as can be seen from the printing of its deinitializer message in the example below:

这次闭包的self捕获是无主引用，不会强制保持闭包捕获的HTMLElement实例。如果你将paragraph变量设为nil，HTMLElement实例会被销毁并会看到由其析构函数打印出的销毁信息，如下所示：

```
paragraph = nil
// prints "p is being deinitialized
```