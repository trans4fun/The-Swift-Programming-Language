##Inheritance
##继承

A class can *inherit* methods, properties, and other characteristics from another class. When one class inherits from another, the inheriting class is known as a *subclass*, and the class it inherits from is known as its *superclass*.

一个类可以从另外一个类中*继承*方法，属性以及其他特性。当一个类继承另外一个类时，这个类被称作为*子类*，而被继承的类被称作为*父类*。

Inheritance is a fundamental behavior that differentiates classes from other types in Swift.
Classes in Swift can call and access methods, properties, and subscripts belonging to their superclass and can provide their own overriding versions of those methods, properties, and subscripts to refine or modify their behavior. Swift helps to ensure your overrides are correct by checking that the override definition has a matching superclass definition.

在Swift语言中，继承是区分类与其他类型的一个基本行为。一个类可以访问并调用其父类中的方法，属性和下标，也可以通过重写它们来修改或优化它们的行为。Swift通过检查重写的定义是否能与一个父类中的定义匹配来确保重写的正确性。

Classes can also add property observers to inherited properties in order to be notified when the value of a property changes. Property observers can be added to any property, regardless of whether it was originally defined as a stored or computed property.

类也可以通过对继承的属性添加观察器来监听它们的变化。属性观察器可以被添加用于监听任何属性，无论被监听的属性最初是被定义为存储属性还是计算属性。

##Defining a Base Class
##定义一个基类

Any class that does not inherit from another class is known as a *base* class.
一个没有继承其他类的类被称为*基类*。

```
NOTE
Swift classes do not inherit from a universal base class. Classes you define without specifying a superclass automatically become base classes for you to build upon.
```

```
注意
Swift中的类没有继承一个全局的基类。没有指定父类的类会自动成为一个可用来被扩展的基类。
```

The example below defines a base class called `Vehicle`. This base class declares two properties(`numberOfWheels` and `maxPassengers`) that are universal to all vehicles. These properties are used by a method called `description`, which returns a `String` description of the vehicle’s characteristics:

下面的例子定义了一个基类`Vehicle`。类中声明了两个所有车辆都通用的属性(`numberOfWheels`和`maxPassengers`)。这两个属性在方法`description`中被使用，这个方法返回一个`String`类型的值来描述车辆的特性。

```
class Vehicle {
  var numberOfWheels: Int
  var maxPassengers: Int
  func description() -> String {
    return "\(numberOfWheels) wheels; up to \(maxPassengers) passengers"
  } 
  init() {
    numberOfWheels = 0
    maxPassengers = 1
  }
}
```

The Vehicle class also defines an initializer to set up its properties. Initializers are described in detail in Initialization, but a brief introduction is required here in order to illustrate how inherited properties can be modified by subclasses.
Vehicle类中还定义了一个构造器来初始化它的属性。构造器在构造过程章节中有详细描述，不过在这里会简单介绍一下被继承的属性是如何被子类修改的。

You use initializers to create a new instance of a type. Although initializers are not methods, they are written in a very similar syntax to instance methods. An initializer prepares a new instance for use, and ensures that all properties of the instance have valid initial values.
构造器会被用来创建一个类型的实例。尽管构造器并不是方法，但是书写它们的语法和实例方法非常类似。构造器准备一个新的实例供使用，并确保实例中所有的属性都有合法的初始值。

In its simplest form, an initializer is like an instance method with no parameters, written using the init keyword:
在最简单的形式中，构造器就像是一个没有参数的实例方法，用关键词init来声明。

1 init() {
2 // perform some initialization here
3 }

To create a new instance of Vehicle, call this initializer with initializer syntax, written as TypeName followed by empty parentheses:
创建一个Vehicle类实例需要通过使用构造器语法来调用构造器，写法是在类名后加上一对空的括号。

let someVehicle = Vehicle()

The initializer for Vehicle sets some initial property values (numberOfWheels = 0 and maxPassengers = 1) for an arbitrary vehicle.
Vehicle类的构造器为一个车辆初始化了一些属性(numberOfWheels = 0 和 maxPassengers = 1)。

The Vehicle class defines common characteristics for an arbitrary vehicle, but is not much use in itself. To make it more useful, you need to refine it to describe more specific kinds of vehicle.
Vehicle类为车辆定义了一些公用的特性，但是这些特性对类本身来说并没有太多作用。为了提高这些特性的可用性，需要描述更多不同特定种类的车辆。

Subclassing
子类化
Subclassing is the act of basing a new class on an existing class. The subclass inherits characteristics from the existing class, which you can refine. You can also add new characteristics to the subclass.
子类化是指在一个已有类的基础上建立一个新的类。新建的子类会继承已有类的特性，并可以优化它们。在子类中还可以增加新的特性。

To indicate that a class has a superclass, write the superclass name after the original class name, separated by a colon:
当声明一个类的父类时，需要将父类的名字写在原有类之后，并用冒号分隔:
1 class SomeClass: SomeSuperclass {
2 // class definition goes here
3 }

The next example defines a second, more specific vehicle called Bicycle. This new class is based on the existing capabilities of Vehicle. You indicate this by placing the name of the class the subclass builds upon (Vehicle) after its own name (Bicycle), separated by a colon.
下面的例子定义了另一个更具体的车辆类Bicycle。新定义的类基于Vehicle类中存在的功能。定义的时候需要把父类的名字(Vehicle)放在新定义类的名字(Bicycle)之后，并用冒号分隔。

This can be read as:
“Define a new class called Bicycle, which inherits the characteristics of Vehicle”:
下面的语句可以这样来解读：
“定义一个新的名为Bicycle的类，它继承了Vehicle类的特性。”
1 class Bicycle: Vehicle {
2 init() {
3 super.init()
4 numberOfWheels = 2
5 }
6 }

Bicycle is a subclass of Vehicle, and Vehicle is the superclass of Bicycle. The new Bicycle class
automatically gains all characteristics of Vehicle, such as its maxPassengers and numberOfWheels properties.You can tailor those characteristics and add new ones to better match the requirements of the Bicycle class.
Bicycle是Vehicle的子类, 反而言之Vehicle是Bicycle的父类. 新创建的Bicycle类自动获得了Vehicle类的所有特性，比如它的maxPassengers与numberOfWheels属性。为了更好的满足Bicycle类的需求，你可以修改这些特性或者增加新的特性。

The Bicycle class also defines an initializer to set up its tailored characteristics. The initializer for Bicycle calls super.init(), the initializer for the Bicycle class’s superclass, Vehicle, and ensures that all of the inherited properties are initialized by Vehicle before Bicycle tries to modify them.
Bicycle类同样定义了一个构造器来初始化其修改过的特性。Bicycle的构造器通过调用其父类Vehicle的构造器super.init()来确保所有继承下来的属性在被修改前都已被Vehicle类成功初始化。

注意
Unlike Objective-C, initializers are not inherited by default in Swift. For more information, see Initializer
Inheritance and Overriding.
与Objective-C不同的是，在Swift中构造器是不会默认被继承的。更多信息请参考构造器的继承和重写。

The default value of maxPassengers provided by Vehicle is already correct for a bicycle, and so it is not changed within the initializer for Bicycle. The original value of numberOfWheels is not correct, however, and is replaced with a new value of 2.
Vehicle类中为maxPassengers提供的默认值对于一辆自行车来说已经是正确的了，所以在Bicycle类的构造器中没有做修改。而numberOfWheels的原始值对于一辆自行车来说是错误的，所以它被替换成了一个新的值2。

As well as inheriting the properties of Vehicle, Bicycle also inherits its methods. If you create an instance of Bicycle, you can call its inherited description method to see how its properties have been updated:
除了继承了Vehicle类中的属性，Bicycle类还继承了它的方法。创建了一个Bicycle的实例后，可以通过调用它继承过来的description方法来观察类中属性的更新。
1 let bicycle = Bicycle()
2 println("Bicycle: \(bicycle.description())")
3 // Bicycle: 2 wheels; up to 1 passengers

Subclasses can themselves be subclassed:
子类可以被继续继承：
1 class Tandem: Bicycle {
2 init() {
3 super.init()
4 maxPassengers = 2
5 }
6 }

This example creates a subclass of Bicycle for a two-seater bicycle known as a “tandem”. Tandem inherits the two properties from Bicycle, which in turn inherits these properties from Vehicle. Tandem doesn’t change the number of wheels—it’s still a bicycle, after all—but it does update maxPassengers to have the correct value for a tandem.
上面的例子创建了一个Bicycle类的子类双人自行车(Tandem)。Tandem类继承了Bicycle类中的两个属性，而这两个属性又是从Vehicle类继承下来的。由于Tandem仍然是自行车的一种，所以类中没有改变车轮数量的属性numberOfWheels，但是它更新了表示最大乘客数的属性maxPassengers以满足一辆双人自行车的要求。

N OT E
Subclasses are only allowed to modify variable properties of superclasses during initialization. You can’t
modify inherited constant properties of subclasses.
注意
在初始化过程中，子类只允许修改父类中的变量属性，而常量属性是不能被修改的。

Creating an instance of Tandem and printing its description shows how its properties have been updated:
下面通过创建一个Tandem的实例并打印其描述来观察它的属性更新：

1 let tandem = Tandem()
2 println("Tandem: \(tandem.description())")
3 // Tandem: 2 wheels; up to 2 passengers

Note that the description method is also inherited by Tandem. Instance methods of a class are inherited by any and all subclasses of that class.
注意description方法也是Tandem类继承下来的。一个类中的实例方法会被它所有的子类继承。

Overriding
重写
A subclass can provide its own custom implementation of an instance method, class method, instance property, or subscript that it would otherwise inherit from a superclass. This is known as overriding.
子类可以为继承过来的实例方法，类方法，实例属性或脚本提供它自己的实现，这个行为被称作重写。

To override a characteristic that would otherwise be inherited, you prefix your overriding definition with the override keyword. Doing so clarifies that you intend to provide an override and have not provided a matching definition by mistake. Overriding by accident can cause unexpected behavior, and any overrides without the override keyword are diagnosed as an error when your code is compiled.
如果要重写某个属性，你需要在重写的定义前加上override关键字。这么做是为了表明你是为了提供一个重写的版本而不是错误地提供了一个同样的定义。意外地重写会引起不可预知的错误，没有加关键字override的重写都会在编译时被诊断为错误。

The override keyword also prompts the Swift compiler to check that your overriding class’s superclass (or one of its parents) has a declaration that matches the one you provided for the override. This check ensures that your overriding definition is correct.
Override关键字也会提醒Swift编译器去校验被继承的父类(或其中中一个父类)中是否有匹配的声明用于被重写。这个检查可以确保你的重写定义是正确的。
Accessing Superclass Methods, Properties, and Subscripts
访问父类的方法，属性和脚本

When you provide a method, property, or subscript override for a subclass, it is sometimes useful to use the existing superclass implementation as part of your override. For example, you can refine the behavior of that existing implementation or store a modified value in an existing inherited variable.
当你访问父类的方法，属性或脚本时，有时在你的重写版本中使用已存在的父类实现会很有作用。比如你可以优化一个已有的实现或者在一个继承来的变量重储存一个修改过的值。

Where this is appropriate, you access the superclass version of a method, property, or subscript by using the super prefix:
在适当的地方，你可以通过super前缀来访问父类版本的方法，属性或脚本：
	An overridden method named someMethod can call the superclass version of someMethod by callingsuper.someMethod() within the overriding method implementation.
一个重写的方法someMethod可以在方法实现中通过super.someMethod()来调用父类版本的someMethod。
	An overridden property called someProperty can access the superclass version of someProperty assuper.someProperty within the overriding getter or setter implementation.
一个重写的属性someProperty可以在getter和setter方法的重写实现中通过super.someProperty来访问父类版本的someProperty。
	An overridden subscript for someIndex can access the superclass version of the same subscript as super[someIndex] from within the overriding subscript implementation.
一个重写的脚本someIndex可以在脚本实现中通过super[someIndex]来调用父类版本的someIndex。

Overriding Methods
重写方法
You can override an inherited instance or class method to provide a tailored or alternative implementation of the method within your subclass.
在子类中你可以通过提供一个定制或替代的实现来重写一个继承过来的实例方法或类方法。
The following example defines a new subclass of Vehicle called Car, which overrides the description method it inherits from Vehicle:
下面的例子定义了Vehicle类的一个新子类Car, 子类中重写了从父类中继承过来的方法description:
1 class Car: Vehicle {
2 var speed: Double = 0.0
3 init() {
4 super.init()
5 maxPassengers = 5
6 numberOfWheels = 4
7 }
8 override func description() -> String {
9 return super.description() + "; "
10 + "traveling at \(speed) mph"
11 }
12 }

Car declares a new stored Double property called speed. This property defaults to 0.0, meaning “zero miles per hour”. Car also has a custom initializer, which sets the maximum number of passengers to 5, and the default number of wheels to 4.
Car类中声明了一个新的Double类存储型属性speed，默认值是0.0，代表”时速为每小时0英里”。Car类还有自定义构造器，构造器中设置最大乘客量为5，默认车轮数为4。

Car overrides its inherited description method by providing a method with the same declaration as the description method from Vehicle. The overriding method definition is prefixed with the override keyword.
Car类重写了继承来的description方法，它的声明和父类Vehicle中一致。被重写的方法定义前加上了override关键字。

Rather than providing a completely custom implementation of description, the overriding method actually starts by calling super.description to retrieve the description provided by Vehicle. It then appends some additional information about the car’s current speed.
重写的方法并没有完全自定义方法description的实现，它在开始时通过调用super.description来使用父类Vehicle中的方法实现，之后再为车辆的当前速度追加了一些额外信息。

If you create a new instance of Car, and print the output of its description method, you can see that the description has indeed changed:
如果你创建一个Car类的实例，并打印description方法的输出，你会发现描述的信息已经发生了改变。
1 let car = Car()
2 println("Car: \(car.description())")
3 // Car: 4 wheels; up to 5 passengers; traveling at 0.0 mph

Overriding Properties
重写属性
You can override an inherited instance or class property to provide your own custom getter and setter for that property, or to add property observers to enable the overriding property to observe when the underlying property value changes.
你可以重写继承来的实例属性或类属性来提供自定义的getter和setter方法，或添加属性观察器来使被重写的属性观察属性值什么时候发生改变。

Overriding Property Getters and Setters
重写属性的Getters和Setters
You can provide a custom getter (and setter, if appropriate) to override any inherited property, regardless of whether the inherited property is implemented as a stored or computed property at its source. The stored or computed nature of an inherited property is not known by a subclass—it only knows that the inherited property has a certain name and type. You must always state both the name and the type of the property you are overriding, to enable the compiler to check that your override matches a superclass property with the same name and type.
你可以提供自定义的getter(或setter,如适用)来重写任何被继承的属性，无论被继承的属性是存储型的还是计算型的。子类并不知道继承来的属性是存储型的还是计算型的，它只知道继承来的属性有名字和类型。在你重写一个属性时，必须声明它的名字和类型。这是为了让编译器检测你重写的属性在父类中有相同的名字和类型。

You can present an inherited read-only property as a read-write property by providing both a getter and a setter in your subclass property override. You cannot, however, present an inherited read-write property as a read-only property.
你可以通过提供getter和setter来将继承来的一个只读属性重写为一个读写属性。但是你无法将一个继承来的读写属性重写成一个只读属性。

N OT E
If you provide a setter as part of a property override, you must also provide a getter for that override. If you don’t want to modify the inherited property’s value within the overriding getter, you can simply pass through the inherited value by returning super.someProperty from the getter, as in the SpeedLimitedCar example below.
注意
如果你在重写时为一个属性提供了setter，那么你必须同时要提供一个getter。如果你不想在重写版本的getter中修改继承来的属性值，你可以直接返回super.someProperty，正如下面SpeedLimitedCar的例子所示。

The following example defines a new class called SpeedLimitedCar, which is a subclass of Car. The SpeedLimitedCar class represents a car that has been fitted with a speed-limiting device, which prevents the car from traveling faster than 40mph. You implement this limitation by overriding the inherited speed property:
下面的例子定义了一个新的类SpeedLimitedCar，这个类是Car类的子类。SpeedLimitedCar类表示安装了限速装置的车来防止车的时速超过40英里。你需要通过重写speed属性来实现这个速度限制：
1 class SpeedLimitedCar: Car {
2 override var speed: Double {
3 get {
4 return super.speed
5 }
6 set {
7 super.speed = min(newValue, 40.0)
8 }
9 }
10 }

Whenever you set the speed property of a SpeedLimitedCar instance, the property’s setter implementation checks the new value and limits it to 40mph. It does this by setting the underlying speed property of its superclass to be the smaller of newValue and 40.0. The smaller of these two values is determined by passing them to the min function, which is a global function provided by the Swift standard library. The min function takes two or more values and returns the smallest one of those values.
当你设置一个SpeedLimitedCar实例的speed属性时，属性的setter方法会检验新设置的值并把它限制在时速40英里以内，这是通过选择新设置的值和40之间最小的值来实现的。这个比较会通过调用min函数实现，它是Swift标准库中的一个方法。min函数接受两个或更多的参数并返回其中最小的一个。

If you try to set the speed property of a SpeedLimitedCar instance to more than 40mph, and then print the output of its description method, you see that the speed has been limited:
如果你尝试将SpeedLimitedCar实例中的speed属性设置成时速40英里以上，然后打印description方法的输出，你会看到车速已经被限制了：
1 let limitedCar = SpeedLimitedCar()
2 limitedCar.speed = 60.0
3 println("SpeedLimitedCar: \(limitedCar.description())")
4 // SpeedLimitedCar: 4 wheels; up to 5 passengers; traveling at 40.0 mph

Overriding Property Observers
覆盖属性观察器
You can use property overriding to add property observers to an inherited property. This enables you to be notified when the value of the inherited property changes, regardless of how that property was originally implemented. For more information on property observers, see Property Observers.
你可以在属性重写时为一个继承来的属性添加属性观察器。当继承来的属性被修改时，你就会被通知到，无论那个属性原来是如何被实现的。关于属性观察器的更多内容，请参考属属性观察器。

N OT E
You cannot add property observers to inherited constant stored properties or inherited read-only computed properties. The value of these properties cannot be set, and so it is not appropriate to provide a willSet or didSet implementation as part of an override. 
Note also that you cannot provide both an overriding setter and an overriding property observer. If you want to observe changes to a property’s value, and you are already providing a custom setter for that property, you can simply observe any value changes from within the custom setter.
注意
你不可以为继承来的常量存储型属性或只读计算型属性添加属性观察器。这些属性的值是不可以被修改的，所以在重写时为它们提供willSet和didSet的实现是不恰当的。
注意你也不能同事提供重写的setter方法和属性观察期。如果你想要观察属性值的变化，并且你已经给那个属性提供了定制的setter方法，在setter方法中你就已经可以观察到任何属性值的变化了。

The following example defines a new class called AutomaticCar, which is a subclass of Car. The AutomaticCar class represents a car with an automatic gearbox, which automatically selects an appropriate gear to use based on the current speed. AutomaticCar also provides a custom description method to print the current gear.
下面的例子定义了一个新类AutomaticCar，它是Car类的子类。AutomaticCar类表示自动档汽车，它会根据当前的车速选择一个合适的档位。AutomaticCar提供了一个定制的description方法来输出当前的档位。
1 class AutomaticCar: Car {
2 var gear = 1
3 override var speed: Double {
4 didSet {
5 gear = Int(speed / 10.0) + 1
6 }
7 }
8 override func description() -> String {
9 return super.description() + " in gear \(gear)"
10 }
11 }

Whenever you set the speed property of an AutomaticCar instance, the property’s didSet observer automatically sets the gear property to an appropriate choice of gear for the new speed. Specifically, the property observer chooses a gear which is the new speed value divided by 10, rounded down to the nearest integer, plus 1. A speed of 10.0 produces a gear of 1, and a speed of 35.0 produces a gear of 4:
当你为一个AutomaticCar实例设置speed属性时，属性的didSet观察器会自动设置gear属性到一个合适的档位。具体的计算方法是，属性观察者将新设置的速度值除以10，向下取整之后再加1。例如速度是10的时候档位是1，速度是35.0的时候档位是4。

1 let automatic = AutomaticCar()
2 automatic.speed = 35.0
3 println("AutomaticCar: \(automatic.description())")
4 // AutomaticCar: 4 wheels; up to 5 passengers; traveling at 35.0 mph in gear 4

Preventing Overrides
防止重写
You can prevent a method, property, or subscript from being overridden by marking it as final. Do this by writing the @final attribute before its introducer keyword (such as @final var, @final func, @final class func, and @final subscript).
你可以通过标记一个属性，方法或附属脚本为final来防止它们被重写。具体方法是在声明它们的关键字前加上@final (例如@final var, @final func, @final class func, @final subscript)。

Any attempts to override a final method, property, or subscript in a subclass are reported as a compile-time error. Methods, properties or subscripts that you add to a class in an extension can also be marked as final within the extension’s definition. 
如果被标记为final的方法，属性或附属脚本在子类中被尝试重写，在编译时便会报错。在扩展时被添加到类中的方法，属性或附属脚本也可以在扩展的定义中标记为final。
You can mark an entire class as final by writing the @final attribute before the class keyword in its class definition (@final class). Any attempts to subclass a final class will be reported as a compile-time error.
你也可以通过在关键字class前添加@final属性(@final class)来把整个类标记为final。如此以来这个类就不可以被继承，否则在编译时会报错。
