## 问题

* `initializer` 的定义？『构造方法』
* `deinitializer` 的定义？『析构方法』
* `Stored Properties` 的定义？『属性值』
* `observers` 的定义？『观察者方法』
* `external name` 的定义？『外部名称』
* `local name` 的定义？『内部名称』
* `constant properties` 的定义？『恒定属性』
* `Optional Property Types` 的定义？『可选属性类型』
* `Memberwise` 的定义？『成员式』
* `Initializer Delegation` 的定义？『构造代理』
* `designated initializers` 的定义？『指定构造方法』
* `convenience initializers` 的定义？『便利构造方法』
* `delegates up` 的定义？『向上委托』
* `nonetheless` 的定义？『仍然』

## 构造过程 (Initialization)

_构造过程_是准备实例化类、结构或枚举的过程。该过程需要为当前实例化对象的每个属性值设置初始值，并且在其准备好之前执行所需的设置或初始化。

> “Initialization is the process of preparing an instance of a class, structure, or enumeration for use. This process involves setting an initial value for each stored property on that instance and performing any other setup or initialization that is required before the new instance is ready to for use.”

你通过定义_构造方法_来实现构造过程，就好比能够创建特定类型的新实例化对象的特殊方法。与 Objective-C 不同的是，Swift 的构造方法没有返回值。其主要作用是保证一个类的新实例在其首次使用之前能够被正确地初始化。

> “You implement this initialization process by defining initializers, which are like special methods that can be called to create a new instance of a particular type. Unlike Objective-C initializers, Swift initializers do not return a value. Their primary role is to ensure that new instances of a type are correctly initialized before they are used for the first time.”

你也可以为类的实例实现一个_析构方法_，这可以让该实例在被释放前执行任意自定义的清理工作。需要了解更多关于析构方法的信息，请见『析构过程』章节。

> “Instances of class types can also implement a deinitializer, which performs any custom cleanup just before an instance of that class is deallocated. For more information about deinitializers, see Deinitialization.”

### 初始化属性值 (Setting Initial Values for Stored Properties)

类和结构都_必须_在该类(或结构)的实例被创建时为其属性值设定合适的初始值。属性值不能是一个不确定的状态。

> “Classes and structures must set all of their stored properties to an appropriate initial value by the time an instance of that class or structure is created. Stored properties cannot be left in an indeterminate state.”

你可以在构造方法中为属性值设定初始值，或者在属性值的定义中指定一个默认值。我们会在接下来的章节中描述这些操作。

> “You can set an initial value for a stored property within an initializer, or by assigning a default property value as part of the property’s definition. These actions are described in the following sections.”

提示：

> 无论是你为属性值指定默认值，还是通过构造方法设定初始值，该属性值的真实值被直接设定，而不会调用属性值观察者方法。
> > “When you assign a default value to a stored property, or set its initial value within an initializer, the value of that property is set directly, without calling any property observers.”

### 构造方法 (Initializers)

_构造方法_用来创建类的新实例对象。其最简单的形式就是使用 `init` 关键字，类似一个没有参数的实例方法。

> “Initializers are called to create a new instance of a particular type. In its simplest form, an initializer is like an instance method with no parameters, written using the init keyword.”

在接下来的例子中定义了一个叫 `Fahrenheit` 的结构来存储用华氏表示的温度。`Fahrenheit` 结构拥有一个类型为 `Double` 的属性值 `temperature`：

> “The example below defines a new structure called Fahrenheit to store temperatures expressed in the Fahrenheit scale. The Fahrenheit structure has one stored property, temperature, which is of type Double:”

```
struct Fahrenheit {
    var temperature: Double
    init() {
        temperature = 32.0
    }
}
var f = Fahrenheit()
println("The default temperature is \(f.temperature)° Fahrenheit")
// prints "The default temperature is 32.0° Fahrenheit
```

该结构只定义了一个不带任何参数的构造方法 `init`，该构造方法为属性值 `temperature` 设定了初始值 `32.0`（在华氏温度中表示水的冰点温度）。

> “The structure defines a single initializer, init, with no parameters, which initializes the stored temperature with a value of 32.0 (the freezing point of water when expressed in the Fahrenheit scale).”

### 默认属性值 (Default Property Values)

如上所示，你可以在一个构造方法中设定属性值的初始值。另外，你也可以在属性值声明时为其指定_默认值_。

> “You can set the initial value of a stored property from within an initializer, as shown above. Alternatively, specify a default property value as part of the property’s declaration. You specify a default property value by assigning an initial value to the property when it is defined.”

提示：

> 如果一个属性值总是拥有相同的初始值，请为其提供默认值，而不是在构造方法中设定初始值。虽然结果是一样的，*但默认值将属性值声明和初始化更紧密地绑在一起。这样不仅更简短，也更清晰，能够让你通过默认值来判断该属性值的数据类型。默认值也能让你更容易理解默认构造方法与构造方法继承，我们会在接下来的章节中描述它们。
> > “If a property always takes the same initial value, provide a default value rather than setting a value within an initializer. The end result is the same, but the default value ties the property’s initialization more closely to its declaration. It makes for shorter, clearer initializers and enables you to infer the type of the property from its default value. The default value also makes it easier for you to take advantage of default initializers and initializer inheritance, as described later in this chapter.”

你可以将上面的 `Fahrenheit` 结构简单写成在属性 `temperature` 被申明时提供一个默认值：

>“You can write the Fahrenheit structure from above in a simpler form by providing a default value for its temperature property at the point that the property is declared:”

```
struct Fahrenheit {
    var temperature = 32.0
}
```

### 自定义构造过程 (Customizing Initialization)

你可以自定义构造过程中的输入参数和可选属性类型，也可以在构造过程中修改常量，我们会在接下来的章节中描述它们。

> “You can customize the initialization process with input parameters and optional property types, or by modifying constant properties during initialization, as described in the following sections.”

#### 初始化参数 (Initialization Parameters)

要自定义构造过程，你可以在构造方法的定义中提供_初始化参数_，并定义其类型和名字。初始化参数的作用和语法与函数和方法的参数相同。

> “You can provide initialization parameters as part of an initializer’s definition, to define the types and names of values that customize the initialization process. Initialization parameters have the same capabilities and syntax as function and method parameters.”

在接下来的例子中定义了一个 `Celsius` 的结构来存储用摄氏表示的温度。`Celsius` 结构实现了两个自定义的构造方法，分别是 `init(fromFahrenheit:)` 和 `init(fromKelvin:)`，能够通过不同的温标值分别初始化该结构的实例。

> “The following example defines a structure called Celsius, which stores temperatures expressed in the Celsius scale. The Celsius structure implements two custom initializers called init(fromFahrenheit:) and init(fromKelvin:), which initialize a new instance of the structure with a value from a different temperature scale:”

```
struct Celsius {
    var temperatureInCelsius: Double = 0.0
    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }
    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
}
let boilingPointOfWater = Celsius(fromFahrenheit: 212.0)
// boilingPointOfWater.temperatureInCelsius is 100.0
let freezingPointOfWater = Celsius(fromKelvin: 273.15)
// freezingPointOfWater.temperatureInCelsius is 0.0
```

第一个构造方法拥有一个外部名称为 `fromFahrenheit` 内部名称为 `fahrenheit` 的初始化参数。第二个构造方法拥有一个外部名称为 `fromKelvin` 内部名称为 `kelvin` 的初始化参数。这两个构造方法都将各自的参数转换为摄氏温标值，并保存在属性值 `temperatureInCelsius` 中。

> “The first initializer has a single initialization parameter with an external name of fromFahrenheit and a local name of fahrenheit. The second initializer has a single initialization parameter with an external name of fromKelvin and a local name of kelvin. Both initializers convert their single argument into a value in the Celsius scale and store this value in a property called temperatureInCelsius.”

##### 参数的外部名称和内部名称 (Local and External Parameter Names)

如同函数和方法的参数一样，初始化参数能同时拥有在构造方法体内使用的内部名称，和构造方法被调用时的外部名称。

> “As with function and method parameters, initialization parameters can have both a local name for use within the initializer’s body and an external name for use when calling the initializer.”

可是，构造方法不像函数和方法那样在其括号前有确定的方法名。因此，初始化参数的类型和名字在明确哪个构造方法被调用时起到了特别重要的作用。正因如此，如果你没有提供外部名称，Swift 会自动为构造方法中的_每个_参数提供外部名称。自动生成的外部名称与内部名称相同，就如你在每个初始化参数前写了 # 符号。

> “However, initializers do not have an identifying function name before their parentheses in the way that functions and methods do. Therefore, the names and types of an initializer’s parameters play a particularly important role in identifying which initializer should be called. Because of this, Swift provides an automatic external name for every parameter in an initializer if you don’t provide an external name yourself. This automatic external name is the same as the local name, as if you had written a hash symbol before every initialization parameter.”

提示：

> 如果你不想在构造方法的参数中提供外部名称，请将下划线(_)作为申明为该参数的外部名称以复写上面描述中的默认行为。
> > “If you do not want to provide an external name for a parameter in an initializer, provide an underscore (_) as an explicit external name for that parameter to override the default behavior described above.”

在接下来的例子中定义了一个 `Color` 的结构，其拥有三个恒定属性 `red`，`green` 和 `blue`。这些属性值在 `0.0` 到 `1.0` 之间，分别用来表示颜色值中的红、绿、蓝数值。

> “The following example defines a structure called Color, with three constant properties called red, green, and blue. These properties store a value between 0.0 and 1.0 to indicate the amount of red, green, and blue in the color.”

`Color` 定义了一个拥有三个 `Double` 类型且参数名合适的构造方法：

> “Color provides an initializer with three appropriately named parameters of type Double:”

```
struct Color {
    let red = 0.0, green = 0.0, blue = 0.0
    init(red: Double, green: Double, blue: Double) {
        self.red   = red
        self.green = green
        self.blue  = blue
    }
}
```

当你创建 `Color` 实例时，你通过这三种颜色名作为外部名称调用该构造方法：

> “Whenever you create a new Color instance, you call its initializer using external names for each of the three color components:”

```
let magenta = Color(red: 1.0, green: 0.0, blue: 1.0)
```

请注意，想不使用外部名称直接调用该构造方法是不可能的。外部名称一旦被定义，在调用时必须使用它，否则会产生编译错误：

> “Note that it is not possible to call this initializer without using the external names. External names must always be used in an intializer if they are defined, and omitting them is a compile-time error:”

``` 
let veryGreen = Color(0.0, 1.0, 0.0)
// this reports a compile-time error - external names are required
```

#### 可选属性类型 (Optional Property Types)

如果你有一个自定义类型的属性值允许设置为『空值』——可能因为该属性值不能在构造过程中赋值，也可能因为在某些时候允许为『空值』——定义该属性值为_可选_类型。可选类型的属性值会被自动初始化为 `nil`，申明该属性值在构造过程有意设定为『空值』。

> “If your custom type has a stored property that is logically allowed to have “no value”—perhaps because its value cannot be set during initialization, or because it is allowed to have “no value” at some later point—declare the property with an optional type. Properties of optional type are automatically initialized with a value of nil, indicating that the property is deliberately intended to have “no value yet” during initialization.”

在接下来的例子中定义了一个 `SurveyQuestion` 的结构，其拥有一个可选的 `String` 类型属性值 `response`：

> “The following example defines a class called SurveyQuestion, with an optional String property called response:”

```
class SurveyQuestion {
    var text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        println(text)
    }
}
let cheeseQuestion = SurveyQuestion(text: "Do you like cheese?")
cheeseQuestion.ask()
// prints "Do you like cheese?"
cheeseQuestion.response = "Yes, I do like cheese.
```

你无法知道一个调查问题的回应直到它被回答了，因此属性值 `response` 被声明为 `String?` 类型，或称 『可选 `String`』。当一个新的 `SurveyQuestion` 实例被初始化时，它会被自动分配默认值 `nil`，表示『空字符串』。

> “The response to a survey question cannot be known until it is asked, and so the response property is declared with a type of String?, or “optional String”. It is automatically assigned a default value of nil, meaning “no string yet”, when a new instance of SurveyQuestion is initialized.”

### 在构造过程中修改恒定属性 (Modifying Constant Properties During Initialization)

你可以在构造过程中的任意时候修改恒定属性的值，只要在构造过程结束前设定为一个明确的值。

> “You can modify the value of a constant property at any point during initialization, as long as it is set to a definite value by the time initialization finishes.”

提示：

> 对于类的实例，一个恒定属性值只能在申明它的类初始化期间进行修改。它不能由子类修改。

> > “For class instances, a constant property can only be modified during initialization by the class that introduces it. It cannot be modified by a subclass.”

你可以修改上面的 `SurveyQuestion` 例子，使问题的 `text` 属性使用一个恒定属性而不是一个可变属性，以表明一旦 `SurveyQuestion` 的实例被创建，问题属性便不能改变。即使 `text` 属性现在是一个恒定属性，它仍然可以在类的构造方法中设定：

> “You can revise the SurveyQuestion example from above to use a constant property rather than a variable property for the text property of the question, to indicate that the question does not change once an instance of SurveyQuestion is created. Even though the text property is now a constant, it can still be set within the class’s initializer:”

```
class SurveyQuestion {
    let text: String
    var response: String?
    init(text: String) {
        self.text = text
    }
    func ask() {
        println(text)
    }
}
let beetsQuestion = SurveyQuestion(text: "How about beets?")
beetsQuestion.ask()
// prints "How about beets?"
beetsQuestion.response = "I also like beets. (But not with cheese.)
```

### 默认构造方法 (Default Initializers)

Swift 为每个结构或基类提供了_默认构造方法_来为它们的所有属性值提供默认值，**?并不提供一个构造方法。默认构造方法简单的创建一个设定了所有属性值为默认值的新实例。

> “Swift provides a default initializer for any structure or base class that provides default values for all of its properties and does not provide at least one initializer itself. The default initializer simply creates a new instance with all of its properties set to their default values.”

在接下来的例子中定义了一个叫 `ShoppingListItem` 的类，其封装了购物清单中一件商品的名字、数量和支付状态：

> “This example defines a class called ShoppingListItem, which encapsulates the name, quantity, and purchase state of an item in a shopping list:”

```
class ShoppingListItem {
    var name: String?
    var quantity = 1
    var purchased = false
}
var item = ShoppingListItem()
```

因为 `ShoppingListItem` 类中所有的属性值都拥有默认值，且这是一个没有父类的基类，`ShoppingListItem` 自动获得了一个默认构造方法，该方法创建一个设定了所有属性值为默认值的新实例。（`name` 属性是一个可选的 `String` 类型属性，因此它自动获得默认值为 `nil`，尽管这个值并没有写在代码中。）上面的例子使用默认构造方法为 `ShoppingListItem` 类创建实例化对象，构造方法语法写作 `ShoppingListItem()` 并将此实例赋值给 `item` 变量。

> “Because all properties of the ShoppingListItem class have default values, and because it is a base class with no superclass, ShoppingListItem automatically gains a default initializer implementation that creates a new instance with all of its properties set to their default values. (The name property is an optional String property, and so it automatically receives a default value of nil, even though this value is not written in the code.) The example above uses the default initializer for the ShoppingListItem class to create a new instance of the class with initializer syntax, written as ShoppingListItem(), and assigns this new instance to a variable called item.”

#### 结构类型的成员式构造方法 (Memberwise Initializers for Structure Types)

除了上面提到的默认构造方法，如果结构类型为其所有属性值提供了默认值且没有自定义构造方法，那么该结构类型自动接收一个_成员式构造方法_。

> “In addition to the default initializers mentioned above, structure types automatically receive a memberwise initializer if they provide default values for all of their stored properties and do not define any of their own custom initializers.”

成员式构造方法是初始化新结构实例的成员属性的一种简写方式。新实例的属性的初始值可以通过名称传递给成员式构造方法。

> “The memberwise initializer is a shorthand way to initialize the member properties of new structure instances. Initial values for the properties of the new instance can be passed to the memberwise initializer by name.”

在接下来的例子中定义了一个叫 `Size` 的结构，其拥有两个属性值分别是 `width` 和 `height`。通过分配了 `0.0` 作为它们的默认值，两个属性均被推断为 `Double` 类型。

> “The example below defines a structure called Size with two properties called width and height. Both properties are inferred to be of type Double by assigning a default value of 0.0.”

由于所有属性值均拥有默认值，`Size` 这个结构自动接受一个成员式构造方法 `init(width:height:)`，你可以通过这个成员式构造方法创建新的 `Size` 实例：

> “Because both stored properties have a default value, the Size structure automatically receives an init(width:height:) memberwise initializer, which you can use to initialize a new Size instance:”

```
struct Size {
    var width = 0.0, height = 0.0
}
let twoByTwo = Size(width: 2.0, height: 2.0)
```

### 值类型的构造代理 (Initializer Delegation for Value Types)

构造方法可以调用其他的构造方法作为实例构造过程的一部分。这个过程称为_构造代理_，其避免了在多个构造方法中的重复代码。“

> “Initializers can call other initializers to perform part of an instance’s initialization. This process, known as initializer delegation, avoids duplicating code across multiple initializers.”

构造代理的工作原理，以及哪些形式的代理是被允许的，针对值类型和类类型是不同的。值类型（结构和枚举）不支持继承，因此他们的构造代理过程比较简单，因为它们只能委托给由它们自己提供的其他构造方法。但是，类类型可以从其他类继承，如『继承』这一章节所描述。这意味着类有更多的责任去确保它们继承了的所有属性值在构造过程中被分配一个合适的值。这些责任将在接下来的『类的继承和初始化』中说明。

> “The rules for how initializer delegation works, and for what forms of delegation are allowed, are different for value types and class types. Value types (structures and enumerations) do not support inheritance, and so their initializer delegation process is relatively simple, because they can only delegate to another initializer that they provide themselves. Classes, however, can inherit from other classes, as described in Inheritance. This means that classes have additional responsibilities for ensuring that all stored properties they inherit are assigned a suitable value during initialization. These responsibilities are described in Class Inheritance and Initialization below.”

对于值类型，当你自定义构造方法时，你使用 `self.init` 来关联同一值类型的其他构造方法。你只能在构造方法中调用 `self.init`。

> “For value types, you use self.init to refer to other initializers from the same value type when writing your own custom initializers. You can only call self.init from within an initializer.”

请注意，如果你为值类型定义一个自定义构造方法，你将不再能够访问该类型的默认构造方法（或成员式构造方法，如果它是一个结构）。这个约束防止一种情况的出现，即你提供了一个更为复杂的构造方法来执行必要的设置，但有人却不小心绕过它使用了自动生成构造方法。

> “Note that if you define a custom initializer for a value type, you will no longer have access to the default initializer (or the memberwise structure initializer, if it is a structure) for that type. This constraint prevents a situation in which you provide a more complex initializer that performs additional essential setup is circumvented by someone accidentally using one of the automatic initializers instead.”

提示：

> 如果你期望你自定义的值类型能够被默认构造方法和成员式构造方法初始化，并且同时也能够被自定义构造方法初始化，把你的自定义构造方法写在扩展中，而不是该值类型源生实现中的一部分。请参见『扩展』章节了解更多信息。

> > “If you want your custom value type to be initializable with the default initializer and memberwise initializer, and also with your own custom initializers, write your custom initializers in an extension rather than as part of the value type’s original implementation. For more information, see Extensions.”

在接下来的例子中定义了一个叫 `Rect` 的结构来表示一个几何矩形。该例子需要 `Size` 和 `Point` 这两个结构的支持，两个结构均使用 `0.0` 作为它们属性值的默认值：

> “The following example defines a custom Rect structure to represent a geometric rectangle. The example requires two supporting structures called Size and Point, both of which provide default values of 0.0 for all of their properties:”

```
struct Size {
    var width = 0.0, height = 0.0
}
struct Point {
    var x = 0.0, y = 0.0
}
```
你可以通过下面三种方式中的一种来初始化 `Rect` 结构：

* 使用 `origin` 和 `size` 的默认属性值
* 提供一个特定的原始点和大小
* 提供一个中心点和大小

这些构造过程选项由三个自定义构造方法提供，它们均定义在 `Rect` 结构中：

> “You can initialize the Rect structure below in one of three ways—by using its default zero-initialized origin and size property values, by providing a specific origin point and size, or by providing a specific center point and size. These initialization options are represented by three custom initializers that are part of the Rect structure’s definition:”

```
struct Rect {
    var origin = Point()
    var size = Size()
    init() {}
    init(origin: Point, size: Size) {
        self.origin = origin
        self.size = size
    }
    init(center: Point, size: Size) {
        let originX = center.x - (size.width / 2)
        let originY = center.y - (size.height / 2)
        self.init(origin: Point(x: originX, y: originY), size: size)
    }
}
```
第一个 `Rect` 构造方法 `init()` 在功能上和没有提供自定义构造方法的默认构造方法一样。该构造方法的方法体是空的且不执行任何构造过程，由一对空的花括号 `{}` 表示。调用该构造方法将返回一个 `Rect` 实例，它的 `origin` 和 `size` 都被初始化为默认值 `Point(x: 0.0, y: 0.0)` 和 `Size(width: 0.0, height: 0.0)`：

> “The first Rect initializer, init(), is functionally the same as the default initializer that the structure would have received if it did not have its own custom initializers. This initializer has an empty body, represented by an empty pair of curly braces {}, and does not perfom any initialization. Calling this initializer returns a Rect instance whose origin and size properties are both initialized with the default values of Point(x: 0.0, y: 0.0) and Size(width: 0.0, height: 0.0) from their property definitions:”

```
let basicRect = Rect()
// basicRect's origin is (0.0, 0.0) and its size is (0.0, 0.0)
```

第二个 `Rect` 构造方法 `init(origin:size:)` 在功能上和没有提供自定义构造方法的成员式构造方法相同。该构造方法简单地将 `origin` 和 `size` 参数分配给恰当的属性值：

> “The second Rect initializer, init(origin:size:), is functionally the same as the memberwise initializer that the structure would have received if it did not have its own custom initializers. This initializer simply assigns the origin and size argument values to the appropriate stored properties:”

```
let originRect = Rect(origin: Point(x: 2.0, y: 2.0),
    size: Size(width: 5.0, height: 5.0))
// originRect's origin is (2.0, 2.0) and its size is (5.0, 5.0)
```

第三个 `Rect` 构造方法 `init(center:size:)` 稍微复杂一些。它从基于中心点和大小值计算相应的原点开始。然后，它调用（或委托）到 `init(origin:size:)` 构造方法，将新的原点和大小保存到合适的属性中：

> “The third Rect initializer, init(center:size:), is slightly more complex. It starts by calculating an appropriate origin point based on a center point and a size value. It then calls (or delegates) to the init(origin:size:) initializer, which stores the new origin and size values in the appropriate properties:”

```
let centerRect = Rect(center: Point(x: 4.0, y: 4.0),
    size: Size(width: 3.0, height: 3.0))
// centerRect's origin is (2.5, 2.5) and its size is (3.0, 3.0)
```

尽管构造方法 `init(center:size:)` 也能够自己将新的 `origin` 和 `size` 分配给合适的属性。可是，构造方法 `init(center:size:)` 使用已经具有相同功能的构造函数来实现更简单（逻辑清楚）。

> “The init(center:size:) initializer could have assigned the new values of origin and size to the appropriate properties itself. However, it is more convenient (and clearer in intent) for the init(center:size:) initializer to take advantage of an existing initializer that already provides exactly that functionality.”

提示：

> 如果你想通过不定义 `init()` 和 `init(origin:size:)` 构造方法来替代例子中的方法，请见『扩展』章节。

> > “For an alternative way to write this example without defining the init() and init(origin:size:) initializers yourself, see Extensions.”

### 类的继承与构造过程

一个类的所有属性值——包括所有它从父类继承的属性——_必须_在构造过程中分配初始值。

> “All of a class’s stored properties—including any properties the class inherits from its superclass—must be assigned an initial value during initialization.”

Swift 定义了两种类类型的构造方法来保证所有的属性值接收到初始值。它们被称为指定构造方法和便利构造方法。

> “Swift defines two kinds of initializers for class types to help ensure all stored properties receive an initial value. These are known as designated initializers and convenience initializers.”

#### 指定构造方法和便利构造方法 (Designated Initializers and Convenience Initializers)

_指定构造方法_是类的主要构造方法。一个指定构造方法完全初始化所有该类申明的属性并调用合适的父类构造方法来继续向上追溯构造过程的父类链。

> “Designated initializers are the primary initializers for a class. A designated initializer fully initializes all properties introduced by that class and calls an appropriate superclass initializer to continue the initialization process up the superclass chain.”

类往往只有少数指定构造方法，而且只有一个指定构造方法也是很常见的。**?指定构造方法是通过构造过程发生的『漏斗』点，并通过其继续向上追溯构造过程的父类链。

> “Classes tend to have very few designated initializers, and it is quite common for a class to have only one. Designated initializers are “funnel” points through which initialization takes place, and through which the initialization process continues up the superclass chain.”

每个类必须至少拥有一个指定构造方法。在某些情况下，这一要求由从父类继承一个或多个指定构造方法满足，这将在接下来的『自动构造方法继承』中说明。

> “Every class must have at least one designated initializer. In some cases, this requirement is satisfied by inheriting one or more designated initializers from a superclass, as described in Automatic Initializer Inheritance below.”

_便利构造方法_是次要的，是类的辅助构造方法。你可以在同一个类下定义一个便利构造方法来调用指定构造方法，该便利构造方法定义了指定构造方法参数的默认值。你也可以定义一个便利构造方法用于创建特定用例或**?输入值类型的实例。

> “Convenience initializers are secondary, supporting initializers for a class. You can define a convenience initializer to call a designated initializer from the same class as the convenience initializer with some of the designated initializer’s parameters set to default values. You can also define a convenience initializer to create an instance of that class for a specific use case or input value type.”

如果你的类不需要便利构造方法，你可以不提供它。每当一个通用构造过程模型的快捷方式能够节省事件或让该类的构造过程的意图更清晰，请使用创建便利构造方法。

> “You do not have to provide convenience initializers if your class does not require them. Create convenience initializers whenever a shortcut to a common initialization pattern will save time or make initialization of the class clearer in intent.”

#### 构造方法链 (Initializer Chaining)

为了简化指定构造方法和便利构造方法的关系，在构造方法委托调用中 Swift 应用了以下三条规则：

> “To simplify the relationships between designated and convenience initializers, Swift applies the following three rules for delegation calls between initializers:”

* __规则一：__指定构造方法只能从其直接父类中调用指定构造方法。
* __规则二：__便利构造方法只能调用_该类自身_定义的其他构造方法。
* __规则三：__便利构造方法必须在最终调用一个指定构造方法。

> * __Rule 1__ “Designated initializers must call a designated initializer from their immediate superclass.”
> * __Rule 2__ “Convenience initializers must call another initializer available in the same class.”
> * __Rule 3__ “Convenience initializers must ultimately end up calling a designated initializer.”

一个简单的方法来记住这些：

* **?指定构造方法必须总是_向上_委托
* **?便利构造方法必须总是_穿过_委托

> “A simple way to remember this is:”
> 
> * “Designated initializers must always delegate up.”
> * “Convenience initializers must always delegate across.”

这些规则如下图所示：

> “These rules are illustrated in the figure below:”

**?插图[1] Page 408

在这里，父类只有一个指定构造方法和两个便利构造方法。一个便利构造方法调用了其中另一个便利构造方法，而该构造方法调用了唯一那个便利构造方法。这符合上面的规则 2 和 3。该父类自身没有父类，因此不适用规则 1。

> “Here, the superclass has a single designated initializer and two convenience initializers. One convenience initializer calls another convenience initializer, which in turn calls the single designated initializer. This satisfies rules 2 and 3 from above. The superclass does not itself have a further superclass, and so rule 1 does not apply.”

上图中的子类拥有两个指定构造方法和一个便利构造方法。这个便利构造方法必须调用那两个指定构造方法中的一个，因为便利构造方法必须调用其类自身的其他构造方法。这符合上面的规则 2 和 3。该子类中两个指定构造方法都必须调用父类中唯一那个指定构造方法，来符合上面的规则 1。

> “The subclass in this figure has two designated initializers and one convenience initializer. The convenience initializer must call one of the two designated initializers, because it can only call another initializer from the same class. This satisfies rules 2 and 3 from above. Both designated initializers must call the single designated initializer from the superclass, to satisfy rule 1 from above.”

提示：

> 这些规则并不会影响你的类用户如何_创建_各类的实例。上图中的任何构造方法都能用于创建其所在类的完整实例。这些规则只会影响你如何写这些类的实现。

> > “These rules don’t affect how users of your classes create instances of each class. Any initializer in the diagram above can be used to create a fully-initialized instance of the class they belong to. The rules only affect how you write the class’s implementation.”

下面的图显示了一个更为复杂的 4 个类的层次结构。它表现了指定构造方法如何在类构造过程中用作『漏斗』点，简化了这些类层级间的相互关联。

> “The figure below shows a more complex class hierarchy for four classes. It illustrates how the designated initializers in this hierarchy act as “funnel” points for class initialization, simplifying the interrelationships among classes in the chain:”

**?插图[2] Page 410

#### 构造过程的两个阶段 (Two-Phase Initialization)

在 Swift 中类的构造过程有两个阶段。在第一个阶段，每个属性值被申明它的类分配一个初始值。一旦每个属性值的初始状态被确认，第二阶段便开始，每个类能够在新实例被认为是可以使用之前进一步制定其属性值。

> “Class initialization in Swift is a two-phase process. In the first phase, each stored property is assigned an initial value by the class that introduced it. Once the initial state for every stored property has been determined, the second phase begins, and each class is given the opportunity to customize its stored properties further before the new instance is considered ready for use.”

构造过程的两个阶段使构造过程更安全，同时仍然给予一个类层级中每个类以完全的灵活性。构造过程的两个阶段防止属性值在它们被初始化之前被访问，并防止属性值被另一个构造方法意外地设置为其他值。

> “The use of a two-phase initialization process makes initialization safe, while still giving complete flexibility to each class in a class hierarchy. Two-phase initialization prevents property values from being accessed before they are initialized, and prevents property values from being set to a different value by another initializer unexpectedly.”

提示：

> Swift 的构造过程的两个阶段和 Objective-C 的构造过程类似。主要的不同之处在第一阶段 Objective-C 分配 0 或 null (如 `0` 或 `nil`) 值给每个属性。Swift 的构造过程更加灵活，因此它可以让你设置自定义初始值，并可以应付 `0` 或 `nil` 不是一个有效默认值的类型。

> > “Swift’s two-phase initialization process is similar to initialization in Objective-C. The main difference is that during phase 1, Objective-C assigns zero or null values (such as 0 or nil) to every property. Swift’s initialization flow is more flexible in that it lets you set custom initial values, and can cope with types for which 0 or nil is not a valid default value.”

Swift 的编译器执行了四个安全检查，来保证构造过程的两个阶段过程中没有错误：

> “Swift’s compiler performs four helpful safety-checks to make sure that two-phase initialization is completed without error:”

* __安全检查一：__指定构造方法必须保证其所在类申明的属性在向上委托到父类构造方法前被初始化。

> * __Safety Check 1__ “A designated initializer must ensure that all of the properties introduced by its class are initialized before it delegates up to a superclass initializer.”

正如上面所提到的，一个对象的内存只会被初始化一次，该对象的所有属性值的初始化状态都是已知的。为了符合这条规范，一个指定构造方法必须保证其所有属性在它脱手给继承链前是已经被初始化了的。

> “As mentioned above, the memory for an object is only considered fully initialized once the initial state of all of its stored properties is known. In order for this rule to be satisfied, a designated initializer must make sure that all its own properties are initialized before it hands off up the chain.”

* __安全检查二：__一个指定构造方法在给继承的属性赋值之前必须向上委托至一个父类的构造方法。如果不是这样，该指定构造方法分配的新值会被父类的构造过程覆盖。
* __安全检查三：__一个便利构造方法必须在给_任何_属性（包裹其所在类定义的属性）赋值前委托给另一个构造方法。如果不是这样，该便利构造方法分配的新值会被其自身类委托的构造方法覆盖。
* __安全检查四：__直到构造过程的第一阶段完成前，任何构造方法都不能调用实例方法，不能读取任何实例属性，或引用自身为一个值。

> * __Safety Check 2__ “A designated initializer must delegate up to a superclass initializer before assigning a value to an inherited property. If it doesn’t, the new value the designated initializer assigns will be overwritten by the superclass as part of its own initialization.”
> * __Safety Check 3__ “A convenience initializer must delegate to another initializer before assigning a value to any property (including properties defined by the same class). If it doesn’t, the new value the convenience initializer assigns will be overwritten by its own class’s designated initializer.”
> * __Safety Check 4__ “An initializer cannot call any instance methods, read the values of any instance properties, or refer to self as a value until after the first phase of initialization is complete.”

在第一阶段完成前，类的实例并不是完全有效的。当在第一阶段结束时，类实例被认为是有效的，属性只能被访问，方法只能被调用，“

> “The class instance is not fully valid until the first phase ends. Properties can only be accessed, and methods can only be called, once the class instance is known to be valid at the end of the first phase.”

下面是构造过程的两个阶段如何基于上面的 4 个安全检查实现的：

> “Here’s how two-phase initialization plays out, based on the four safety checks above:”

##### 第一阶段

* 一个指定或便利构造方法在一个类中被调用。
* 该类的一个新实例内存被分配。但内存还未被初始化。
* 该类的一个指定构造方法确保该类中申明的所有属性值拥有一个值。这些属性值的内存现在被初始化了。
* 该指定构造方法脱手给父类的构造方法来为它拥有的属性值执行相同的任务。
* 该过程持续向上追溯继承链，直到到达链条顶端。
* 一旦达到继承链的顶端，最终的类必须保证其所有的属性值都拥有一个值，然后该实例的内存被认为是完全初始化的，第一阶段结束。

> * “A designated or convenience initializer is called on a class.”
> * “Memory for a new instance of that class is allocated. The memory is not yet initialized.”
> * “A designated initializer for that class confirms that all stored properties introduced by that class have a value. The memory for these stored properties is now initialized.”
> * “The designated initializer hands off to a superclass initializer to perform the same task for its own stored properties.”
> * “This continues up the class inheritance chain until the top of the chain is reached.”
> * “Once the top of the chain is reached, and the final class in the chain has ensured that all of its stored properties have a value, the instance’s memory is considered to be fully initialized, and phase 1 is complete.”

##### 第二阶段

* 从继承链的顶端向下工作，继承链中每个指定构造方法都能够进一步自定义该实例。现在构造方法可以访问 `self` 并且能够修改其属性，调用实例方法，等等。
* 最后，继承链中每个便利构造方法能够自定义该实例，并且使用 `self` 操作。

> * “Working back down from the top of the chain, each designated initializer in the chain has the option to customize the instance further. Initializers are now able to access self and can modify its properties, call its instance methods, and so on.”
> * “Finally, any convenience initializers in the chain have the option to customize the instance and to work with self.”

下图显示了第一阶段在假想的子类和父类中如何寻找构造过程的调用：

> “Here’s how phase 1 looks for an initialization call for a hypothetical subclass and superclass:”

**?插图[3] Page 415

在这个例子中，构造过程开始于对子类中便利构造方法的调用。该便利构造方法当前还不能修改任何属性。它委托给同一类下的一个指定构造方法。

> “In this example, initialization begins with a call to a convenience initializer on the subclass. This convenience initializer cannot yet modify any properties. It delegates across to a designated initializer from the same class.”

该指定构造方法确保所有子类中的属性都拥有一个值，如安全检查 1。然后它调用了父类的一个指定构造方法来继续向上追溯构造过程。

> “The designated initializer makes sure that all of the subclass’s properties have a value, as per safety check 1. It then calls a designated initializer on its superclass to continue the initialization up the chain.”

父类的指定构造方法确保了父类的所有属性都拥有一个值。在没有往上的父类可以追溯，也不需要进一步的委托。

> “The superclass’s designated initializer makes sure that all of the superclass properties have a value. There are no further superclasses to initialize, and so no further delegation is needed.”

在所有的父类属性都拥有值的时候，内存被认为完全初始化，第一阶段结束。

> “As soon as all properties of the superclass have an initial value, its memory is considered fully initialized, and Phase 1 is complete.”

下图显示了第二阶段如何寻找构造过程的调用：

> “Here’s how phase 2 looks for the same initialization call:”

**?插图[4] Page 416

父类的指定构造方法已经可以进一步自定义实例（这不是必须的）。

> “The superclass’s designated initializer now has an opportunity to customize the instance further (although it does not have to).”

一旦父类的指定构造方法结束，子类的指定构造方法便可执行额外的自定义操作（同样的，这不是必须的）。

> “Once the superclass’s designated initializer is finished, the subclass’s designated initializer can perform additional customization (although again, it does not have to).”

最后，一旦子类的指定构造方法结束，最早被调用的便利构造方法可以执行额外的自定义操作了。

> “Finally, once the subclass’s designated initializer is finished, the convenience initializer that was originally called can perform additional customization.”

#### 构造方法的继承与重写 (Initializer Inheritance and Overriding)

与 Objective-C 的子类不同，Swift 的子类会默认继承它们父类的构造方法。Swift 可以防止一种情况：一个简单的父类构造方法被一个更专业的子类自动继承，并用于创建不完整或不正确的子类实例。

> “Unlike subclasses in Objective-C, Swift subclasses do not not inherit their superclass initializers by default. Swift’s approach prevents a situation in which a simple initializer from a superclass is automatically inherited by a more specialized subclass and is used to create a new instance of the subclass that is not fully or correctly initialized.”

如果你希望你的自定义子类能够提供一个多个与父类相同的构造方法——可能在构造过程中需要一些自定义——你可以在你自定义的子类中提供一个相同构造方法的重写来实现。

> “If you want your custom subclass to present one or more of the same initializers as its superclass—perhaps to perform some customization during initialization—you can provide an overriding implementation of the same initializer within your custom subclass.”

如果你重写的构造方法是一个指定构造方法，你可以在你的子类中重写它的实现，并且能够在子类的重写版方法中调用父类父类版方法。

> “If the initializer you are overriding is a designated initializer, you can override its implementation in your subclass and call the superclass version of the initializer from within your overriding version.”

如果你重写的构造方法是一个便利构造方法，你重写的方法必须调用子类自身申明的另一个指定构造方法，正如前面『构造方法链』说明的规则那样。

> “If the initializer you are overriding is a convenience initializer, your override must call another designated initializer from its own subclass, as per the rules described above in Initializer Chaining.”

提示：

> 与方法、属性和下标不同，当你重写一个构造方法时不需要写 `override` 关键字。

> > “Unlike methods, properties, and subscripts, you do not need to write the override keyword when overriding an initializer.”

#### 自动继承构造方法 (Automatic Initializer Inheritance)

正如上面所描述的，子类会默认继承它们父类的构造方法。可是，在某些情况下，父类的构造方法会被自动继承。在实践中，**?这意味着​​在许多常见情况下你不需要重写构造方法，并且可以最小影响地继承父类的构造方法，这样做是安全。

> “As mentioned above, subclasses do not not inherit their superclass initializers by default. However, superclass initializers are automatically inherited if certain conditions are met. In practice, this means that you do not need to write initializer overrides in many common scenarios, and can inherit your superclass initializers with minimal effort whenever it is safe to do so.”

假设你为你的子类中申明的任何新属性提供默认值，有下面两个规则要遵守：

> “Assuming that you provide default values for any new properties you introduce in a subclass, the following two rules apply:”

* __规则一：__如果你的子类没有定义任何指定构造方法，它会自动继承父类所有的指定构造方法。
* __规则二：__如果你的子类提供了其父类所有的指定构造方法的实现——或者仅仅如『规则一』所说的继承它们，或者在其自身定义中提供自定义的实现——那么该子类会自动继承父类所有的便利构造方法。

> * __Rule 1__ “If your subclass doesn’t define any designated initializers, it automatically inherits all of its superclass designated initializers.”
> * __Rule 2__ “If your subclass provides an implementation of all of its superclass designated initializers—either by inheriting them as per rule 1, or by providing a custom implementation as part of its definition—then it automatically inherits all of the superclass convenience initializers.”

即使你在子类中添加了更多的便利构造方法，这两个规则依然适用。

> “These rules apply even if your subclass adds further convenience initializers.”

提示：

> 一个子类可以实现一个父类的指定构造方法为子类的一个便利构造方法，这是符合『规则二』的。

> > “A subclass can implement a superclass designated initializer as a subclass convenience initializer as part of satisfying rule 2.”

#### 指定与便利构造方法的语法 (Syntax for Designated and Convenience Initializers)

类的指定构造方法的编写方法如值类型的构造方法一样简单：

> “Designated initializers for classes are written in the same way as simple initializers for value types:”

```
init(parameters) {
    statements
}
```

便利构造方法的编写方法也是如此，但必须在 `init` 关键字前面加上 `convenience` 关键字，并以空格分隔：

> “Convenience initializers are written in the same style, but with the convenience keyword placed before the init keyword, separated by a space:”

```
convenience init(parameters) {
    statements
}
```

#### 指定与便利构造方法的行为 (Designated and Convenience Initializers in Action)

在接下来的例子显示了指定构造方法，便利构造方法和自动继承的构造方法的行为。这个例子定义了叫 `Food`，`RecipeIngredient` 和 `ShoppingListItem` 三个类的层级关系，并示范了它们之间是如何相互作用的。

> “The following example shows designated initializers, convenience initializers, and automatic initializer inheritance in action. This example defines a hierarchy of three classes called Food, RecipeIngredient, and ShoppingListItem, and demonstrates how their initializers interact.”

该层级中的基类是 `Food`，它是一个仅仅描述了食物名字的简单类。`Food` 类仅有一个 `String` 类型的属性 `name`，并有两个构造方法来创造 `Food` 的实例：

> “The base class in the hierarchy is called Food, which is a simple class to encapsulate the name of a foodstuff. The Food class introduces a single String property called name and provides two initializers for creating Food instances:”

```
class Food {
    var name: String
    init(name: String) {
        self.name = name
    }
    convenience init() {
        self.init(name: "[Unnamed]")
    }
}
```

下图显示了 `Food` 类的构造方法链：

> “The figure below shows the initializer chain for the Food class:”

**?插图[5] Page 421

类并没有默认的成员式构造方法，因此 `Food` 类提供了一个仅拥有一个 `name` 参数的指定构造方法。该构造方法可以用来创建指定了名字的 `Food` 实例：

```
let namedMeat = Food(name: "Bacon")
// namedMeat's name is "Bacon"
```

在 `Food` 类中的 `init(name: String)` 构造方法是一个_指定构造方法_，因为它保证了 `Food` 实例中的所有属性值是完全初始化的。`Food` 并没有父类，因此构造方法 `init(name: String)` 并不需要在其构造过程中调用 `super.init()`。

> “The init(name: String) initializer from the Food class is provided as a designated initializer, because it ensures that all stored properties of a new Food instance are fully initialized. The Food class does not have a superclass, and so the init(name: String) initializer does not need to call super.init() to complete its initialization.”

该 `Food` 类也提供了一个没有参数的_便利构造方法_ `init()`。构造方法 `init()` 通过将赋值为 `[Unnamed]` 的 `name` 参数委托给 `Food` 类的 `init(name: String)`，提供了食物的默认名字：

> “The Food class also provides a convenience initializer, init(), with no arguments. The init() initializer provides a default placeholder name for a new food by delegating across to the Food class’s init(name: String) with a name value of [Unnamed]:”

```
let mysteryMeat = Food()
// mysteryMeat's name is "[Unnamed]"
```

该层级中的第二个类是 `Food` 的一个子类，叫做 `RecipeIngredient`。该 `RecipeIngredient` 类创建了一个烹饪食谱的原料模型。它申明了一个 `Int` 类型的属性 `quantity`（从 `Food` 中继承了 `name` 属性）并定义了两个构造方法来创建 `RecipeIngredient` 实例：

> “The second class in the hierarchy is a subclass of Food called RecipeIngredient. The RecipeIngredient class models an ingredient in a cooking recipe. It introduces an Int property called quantity (in addition to the name property it inherits from Food) and defines two initializers for creating RecipeIngredient instances:”

```
class RecipeIngredient: Food {
    var quantity: Int
    init(name: String, quantity: Int) {
        self.quantity = quantity
        super.init(name: name)
    }
    convenience init(name: String) {
        self.init(name: name, quantity: 1)
    }
}
```

下图显示了 `RecipeIngredient` 类的构造方法链：

> “The figure below shows the initializer chain for the RecipeIngredient class:”

**?插图[6] Page 423

类 `RecipeIngredient` 拥有唯一一个指定构造方法 `init(name: String, quantity: Int)`，它可以完成新 `RecipeIngredient` 实例的所有属性的填充。该构造方法开始于将传入的 `quantity` 参数赋值给在 `RecipeIngredient` 中申明的新属性 `quantity`。而后，该构造方法向上委托给 `Food` 的构造方法 `init(name: String)`。该过程符合之前『构造过程的两个阶段』章节中的安全检查 1。

> “The RecipeIngredient class has a single designated initializer, init(name: String, quantity: Int), which can be used to populate all of the properties of a new RecipeIngredient instance. This initializer starts by assigning the passed quantity argument to the quantity property, which is the only new property introduced by RecipeIngredient. After doing so, the initializer delegates up to the init(name: String) initializer of the Food class. This process satisfies safety check 1 from Two-Phase Initialization above.”

同时 `RecipeIngredient` 定义了一个便利构造方法 `init(name: String)`，它用于只使用名字来创建 `RecipeIngredient` 实例。该便利构造方法假定了所有没有明确数量的 `RecipeIngredient` 实例的数量为 `1`。该构造方法的定义使创建 `RecipeIngredient` 更加便捷快速，并能够避免创造多个单数量 `RecipeIngredient` 实例时产生的代码冗余。该便利构造方法简单得委托给了其所在类的指定构造方法。

> “RecipeIngredient also defines a convenience initializer, init(name: String), which is used to create a RecipeIngredient instance by name alone. This convenience initializer assumes a quantity of 1 for any RecipeIngredient instance that is created without an explicit quantity. The definition of this convenience initializer makes RecipeIngredient instances quicker and more convenient to create, and avoids code duplication when creating several single-quantity RecipeIngredient instances. This convenience initializer simply delegates across to the class’s designated initializer.”

请注意，`RecipeIngredient` 类提供的便利构造方法 `init(name: String)` 使用了与 `Food` 类中制_指定构造方法_ `init(name: String)` 一样的参数。尽管 `RecipeIngredient` 将其作为便利构造方法，`RecipeIngredient` 仍然提供了其父类所有指定构造方法的实现。因此，`RecipeIngredient` 自动继承了其父类所有的便利构造方法。

> “Note that the init(name: String) convenience initializer provided by RecipeIngredient takes the same parameters as the init(name: String) designated initializer from Food. Even though RecipeIngredient provides this initializer as a convenience initializer, RecipeIngredient has nonetheless provided an implementation of all of its superclass’s designated initializers. Therefore, RecipeIngredient automatically inherits all of its superclass’s convenience initializers too.”

在这个例子中，`RecipeIngredient` 的父类是 `Food`，`Food` 只有一个叫 `init()` 的便利构造方法。因此该构造方法被 `RecipeIngredient` 所继承。继承了的 `init()` 方法和 `Food` 中的一样，只是它委托的是 `RecipeIngredient` 中的 `init(name: String)` 而不是 `Food` 中的。

> “In this example, the superclass for RecipeIngredient is Food, which has a single convenience initializer called init(). This initializer is therefore inherited by RecipeIngredient. The inherited version of init() functions in exactly the same way as the Food version, except that it delegates to the RecipeIngredient version of init(name: String) rather than the Food version.”

这三种构造方法均可以用于创建 `RecipeIngredient` 对象：

> “All three of these initializers can be used to create new RecipeIngredient instances:”

```
let oneMysteryItem = RecipeIngredient()
let oneBacon = RecipeIngredient(name: "Bacon")
let sixEggs = RecipeIngredient(name: "Eggs", quantity: 6)
```

第三个并且是最后一个类是 `RecipeIngredient` 的子类，叫做 `ShoppingListItem`。该 `ShoppingListItem` 类创建了一个食谱购物清单的模型。

> “The third and final class in the hierarchy is a subclass of RecipeIngredient called ShoppingListItem. The ShoppingListItem class models a recipe ingredient as it appears in a shopping list.”

购物清单中的所有商品的初始状态都是『未支付』。为了实现它，`ShoppingListItem` 申明了一个默认值为 `false` 的 `Boolean` 的属性 `purchased`。同时，`ShoppingListItem` 也申明了一个计算过的 `description` 属性，它提供了对 `ShoppingListItem` 实例的文本描述：

> “Every item in the shopping list starts out as “unpurchased”. To represent this fact, ShoppingListItem introduces a Boolean property called purchased, with a default value of false. ShoppingListItem also adds a computed description property, which provides a textual description of a ShoppingListItem instance:”

```
class ShoppingListItem: RecipeIngredient {
    var purchased = false
    var description: String {
    var output = "\(quantity) x \(name.lowercaseString)"
        output += purchased ? " ✔" : " ✘"
        return output
    }
}
```

提示：

> `ShoppingListItem` 并没有定义为 `purchased` 提供初始值的构造方法，因为在购物清单中的商品（按这里的模型）的初始状态总是未支付。

> > “ShoppingListItem does not define an initializer to provide an initial value for purchased, because items in a shopping list (as modeled here) always start out unpurchased.”

因为 `ShoppingListItem` 为所有其申明的属性均提供了默认值，并且其自身没有定义任何构造方法。`ShoppingListItem` 自动继承了其父类的所有指定和便利构造方法。

> “Because it provides a default value for all of the properties it introduces and does not define any initializers itself, ShoppingListItem automatically inherits all of the designated and convenience initializers from its superclass.”

下图显示了这三个类的构造方法链的概览：

> “The figure below shows the overall initializer chain for all three classes:”

**?插图[7] Page 427

这三个继承的构造方法均可以用于创建 `ShoppingListItem` 对象：

> “You can use all three of the inherited initializers to create a new ShoppingListItem instance:”

```
var breakfastList = [
    ShoppingListItem(),
    ShoppingListItem(name: "Bacon"),
    ShoppingListItem(name: "Eggs", quantity: 6),
]
breakfastList[0].name = "Orange juice"
breakfastList[0].purchased = true
for item in breakfastList {
    println(item.description)
}
// 1 x orange juice ✔
// 1 x bacon ✘
// 6 x eggs ✘
```

至此，一个包含了三个新 `ShoppingListItem` 实例的数组 `breakfastList` 被创建出来。这个数组的类型被推断为 `ShoppingListItem[]`。在该数组被创建后，该数组的第一个 `ShoppingListItem` 实例的名字从 `[Unnamed]` 改变为 `Orange`，并且其被标记为已支付状态。输出数组中每个实例的详细描述，显示出它们的默认状态均被按预期地设置了。

> “Here, a new array called breakfastList is created from an array literal containing three new ShoppingListItem instances. The type of the array is inferred to be ShoppingListItem[]. After the array is created, the name of the ShoppingListItem at the start of the array is changed from "[Unnamed]" to "Orange juice" and it is marked as having been purchased. Printing the description of each item in the array shows that their default states have been set as expected.”

### 通过闭包或方法设置默认属性 (Setting a Default Property Value with a Closure or Function)

如果一个属性值的默认值需要一些自定义或者设置，你可以使用闭包或者全局方法来为该属性提供自定义默认值。无论该属性所在类的实例何时被初始化，闭包或方法会被调用，并且其返回值会被分配给该属性作为默认值。

> “If a stored property’s default value requires some customization or setup, you can use a closure or global function to provide a customized default value for that property. Whenever a new instance of the type that the property belongs to is initialized, the closure or function is called, and its return value is assigned as the property’s default value.”

这种类型的闭包和方法为该属性创建了一个相同类型的临时值，**?定制的该值是初始状态所期望的，然后返回这个临时值作为该属性的默认值。

> “These kinds of closures or functions typically create a temporary value of the same type as the property, tailor that value to represent the desired initial state, and then return that temporary value to be used as the property’s default value.”

下面是一个如何使用闭包给属性提供默认值的概览：

> “Here’s a skeleton outline of how a closure can be used to provide a default property value:”

```
class SomeClass {
    let someProperty: SomeType = {
        // create a default value for someProperty inside this closure
        // someValue must be of the same type as SomeType
        return someValue
        }()
}
```

请注意，闭包结束的花括号后面紧跟着一堆空的圆括号。这会告诉 Swift 立即执行该闭包。如果你漏掉了圆括号，你会把闭包本身赋值给该属性，而不是这个闭包的返回值。

> “Note that the closure’s end curly brace is followed by an empty pair of parentheses. This tells Swift to execute the closure immediately. If you omit these parentheses, you are trying to assign the closure itself to the property, and not the return value of the closure.”

提示：

> 如果你使用一个闭包来初始化一个属性，请记住，在该闭包被执行的时候该实例的其他部分还没有被初始化。这意味着你无法在闭包中访问任何其他属性，即使这些属性有默认值也不行。你也不能使用 `self` 属性，或调用任何实例方法。

> > “If you use a closure to initialize a property, remember that the rest of the instance has not yet been initialized at the point that the closure is executed. This means that you cannot access any other property values from within your closure, even if those properties have default values. You also cannot use the implicit self property, or call any of the instance’s methods.”

在接下来的例子中定义了一个叫 `Checkerboard` 的结构，它创建了一个_跳棋_游戏桌面的模型：

> “The example below defines a structure called Checkerboard, which models a board for the game of Checkers (also known as Draughts):”

**?插图[8] Page 431

_跳棋_游戏在一个黑白相间的 10x10 方格的桌面上进行。为了表示这个游戏桌面，`Checkerboard` 结构有唯一一个属性 `boardColors`，该属性是一个拥有 100 个 `Bool` 值的数组。数组中的 `true` 值表示一个黑色方块，`false` 表示一个白色方块。数组中的第一个对象表示桌面左上角的方块，最后一个对象表示桌面右下角的方块。

> “The game of Checkers is played on a ten-by-ten board, with alternating black and white squares. To represent this game board, the Checkerboard structure has a single property called boardColors, which is an array of 100 Bool values. A value of true in the array represents a black square and a value of false represents a white square. The first item in the array represents the top left square on the board and the last item in the array represents the bottom right square on the board.”

`boardColors` 数组由一个闭包来初始化其颜色值：

> “The boardColors array is initialized with a closure to set up its color values:”

```
struct Checkerboard {
    let boardColors: Bool[] = {
        var temporaryBoard = Bool[]()
        var isBlack = false
        for i in 1...10 {
            for j in 1...10 {
                temporaryBoard.append(isBlack)
                isBlack = !isBlack
            }
            isBlack = !isBlack
        }
        return temporaryBoard
        }()
    func squareIsBlackAtRow(row: Int, column: Int) -> Bool {
        return boardColors[(row * 10) + column]
    }
}
```

每当一个新的 `Checkerboard` 实例创建时，该闭包被执行，`boardColors` 的默认值被计算并返回。上面这个例子中的闭包为游戏桌面的每个方块计算并设置合适的颜色值存放在叫 `temporaryBoard` 的临时数组中，并在设置结束后返回这个临时数组作为返回值。该返回的数组保存在 `boardColors` 中，并能够在实例方法 `squareIsBlackAtRow` 中使用。

> “Whenever a new Checkerboard instance is created, the closure is executed, and the default value of boardColors is calculated and returned. The closure in the example above calculates and sets the appropriate color for each square on the board in a temporary array called temporaryBoard, and returns this temporary array as the closure’s return value once its setup is complete. The returned array value is stored in boardColors and can be queried with the squareIsBlackAtRow utility function:”

```
let board = Checkerboard()
println(board.squareIsBlackAtRow(0, column: 1))
// prints "true"
println(board.squareIsBlackAtRow(9, column: 9))
// prints "false"
```





