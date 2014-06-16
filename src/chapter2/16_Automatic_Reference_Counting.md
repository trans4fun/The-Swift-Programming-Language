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

当你创建一个类实例的时候，ARC会为之分配一块内存来存储该实例的相关信息。这些信息包括：该实例的类型及其相关的属性和值。当该实例不再需要的时候，ARC会释放其占用的内存留作他用。这种机制保证了不需要的类实例占用内存会及时得到释放。

However, if ARC were to deallocate an instance that was still in use, it would no longer be possible to access that instance’s properties, or call that instance’s methods. Indeed, if you tried to access the instance, your app would most likely crash.

To make sure that instances don’t disappear while they are still needed, ARC tracks how many properties, constants, and variables are currently referring to each class instance. ARC will not deallocate an instance as long as at least one active reference to that instance still exists.

然而，如果ARC释放了一个正在使用的类实例的内存，那会导致该实例的方法和属性都不能访问。而且，如果你试图访问已被ARC释放的实例，你的APP很可能会崩溃。

为了确保使用中的类实例不会无端消失（被ARC回收），ARC会跟踪和统计每个类实例被多少属性，常量，变量所引用。即使只有一个活动引用存在，该类实例也不会被ARC回收。

To make this possible, whenever you assign a class instance to a property, constant, or variable, that property, constant, or variable makes a strong reference to the instance. The reference is called a “strong“ reference because it keeps a firm hold on that instance, and does not allow it to be deallocated for as long as that strong reference remains.

为了保证ARC机制的有效运行，无论何时你将一个类实例分配给一个属性、常量或一个变量，那么这个属性、常量或变量与类实例之间将建立起一种强引用关系。之所以称为“强引用”，是它会牢牢保持与类实例的引用关系，只要指向类实例的强引用存在，该实例就是不允许被销毁的。
