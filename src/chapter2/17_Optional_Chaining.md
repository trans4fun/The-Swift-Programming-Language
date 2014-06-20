> 翻译：[zearlin](https://github.com/zearlin)  

# Optional Chaining
-----------------

可选链（Optional Chaining）是针对当前可能为空值（`nil`）的可选元素的属性，方法及下标调用和查寻的一种处理。 若可选元素为赋值对应的属性，方法或下标都会被成功调用；反之当可选成员为空值（`nil`）时，侧其属性，方法或下标调为会返回空值（`nil`）。多个的查寻可一起链式调用，并当链路的任意一环为nil时链路调用失败。

> 注意：  
Swift中的可选链与Object-C中空值的方法调用相似，是一种更为全面的实现，适用于所有的类型及支持调用成功与否的判断。

## 可选链，强制解析的一种替代方案

当你想调用一个属性，方法或下标时通过在可选元素（`optional value`）后添置一个问号（?）来声明一个为可选链，当可选元素为非空时，侧与通过添置感叹号（!）来强解析其值的做法非常相似。主要的区别在于当可选元素为空时可选链会得体地以调用失败结束，而强制解析则会引发一个运行时错误。

考虑到可选链空值调用这一情况，可选链的返回值一定为可选值，即使你所查寻的属性，方法或下标返回的并不是是一个可选值。你可以通过返回的可选值来判断可选链的调用是成功的（返回的可选元素有值），还是因为链式中的空值元素而调用失败（返回的可选元素为空）。

具体来说，可选链的返回值类型与预期的返回值类型一致，但封装为了一个可选元素。原本返回为整型的属性，在可选链调用中会返回为可选整型(Int?)

我们将在后续的几个代码片段中解释可选链与强制解析的区别及让你了解如果判断调用成功与否。

首先，我们先定义Person与Residence两个类：

```swift
class Person {
    var residence: Residence?
}

class Residence {
    var numberOfRooms = 1
}
```

`Residence`实例拥有一个命名为`numberOfRooms`的整型属性。而`Person`实例有一个可选属性`residence`其类型为`Residence?`。

如果你创建一个新的`Person`实例，它的`residence`属性由于是被定义为可选型的，此属性将默认初始化为空。下面的代码中，john的residence属性值为空：


```swift
let john = Person()
```

如果你在`residence`后添置感叹号（`!`）以强制解析的方式来访问`person`的`residence`的属性`numberOfRooms`时，会引发一个运行时错误，因为`residence`为空无法被解析。

```swift
let roomCount = john.residence!.numberOfRooms
//将导致运行时错误
```
当`john.residence`为非空及为`roomCount`设一个可理的房间数时以述的代码会被成功调用。然后如上面所演示的，当`residence`为空这段代码就会触发一个运行时错误。

可选链提供了访问`numberOfRooms`值的另一种方式。 在这里通过以问号来取代先前的感叹号以可选链的方式调用。

```swift
if let roomCount = john.residence?.numberOfRooms {
    println("John's residence has \(roomCount) room(s).")
} else {
	println("Unable to retrieve the number of rooms.")
}
// 打印 "Unable to retrieve the number of rooms.
```

这将告诉Swift将可选的`residence`属于链式中的一环并得到`numberOfRooms`的值当`residence`存在时。

因为尝试访问`numberOfRooms`时存在失败的可能，所以可选链返回一个类型为`Int?` 或称之为“可选整型”的值。 当`residence`为空时，这个可选整型也将为空，以表示`numberOfRooms`无法被访问。

需要注意一点即使`numberOfRooms`为非可选整型。通来可选链的方式来调用`numberOfRooms`的值查询时返回的类型是`Int?`而不是一个常规的`Int`。

我们给`john.residence`分配一个`Residence`实例让它不在为一个空值：

```swift
john.residence = Residence()
```

此时`john.residence`包含了一个真实的`Residence`实例而不再为空了。如果你以先前相同的可选链方式去访问`numberOfRooms`，它将返回一个包含默认值 1 的`Int?`：

```swift
if let roomCount = john.residence?.numberOfRooms {
    println("John's residence has \(roomCount) room(s).")
} else {
    println("Unable to retrieve the number of rooms.")
}
// 打印 "John's residence has 1 room(s)"。
```

##定义可选链的模型（实体）类

可选链支持多层的属性，方法及下标调用。这一特性让你可以进一步的调用关联类型的复杂模型中的子属性及判断这些子属性对应的属性，方法及下标下否可以访问。

在下面的代码片段中为后续的几个例子使用定义了四个实体类，这些类都是基于`Person`和`Residence`模型通过增加`Room`及`Address`类及一些相关的属性，方法及下标进行扩展的。

`Person`类还是于先前定义的相同：

```swift
class Person {
    var residence: Residence?
}
```

`Residence `类比之前复杂些。这次我们为 `Residence `声明了一个名为 `rooms `的变量，其初始值为 `Room[] `类型的空数值。

```swift
class Residence {
    var rooms = Room[]()
    var numberOfRooms: Int {
    return rooms.count
    }
    subscript(i: Int) -> Room {
        return rooms[i]
    }
    func printNumberOfRooms() {
        println("The number of rooms is \(numberOfRooms)")
    }
    var address: Address?
}
```
因为在这一版的`Residence`中存储了一个Room实例数组，所以其`numberOfRooms`属性以计算属性的方式实现。计算的`numberOfRooms`属性只是简单的返回了`rooms`数组的`count`属性。

为了更便捷的访问它的`rooms`数组，在这一版中`Residence`提供了一个只读下标，一开始我们假设传参的引索是有效的。如果索引是有效的，下标将返回`rooms`数组与请求索引相对应的`room`对象。

`Residence`还提供了一个名为`printNumberOfRooms`的方法，用于简单地打印房间数。

最后，`Residence`还定义了一个类型为`Address?`的可选属性`address`，对应的`Address`类会在下文中定义。

`rooms`数组中用到的`Room`类非常简单只拥有一个`name`属性及对应设置房间名的构造器。

```swift
class Room {
    let name: String
    init(name: String) { self.name = name }
}
```

模型中最后的一个类叫`Address`。类中有三个类型为`String?`的可选属性。作为地址信息中的一部分头两个属性`buildingName`及`buildingNumber`是两个可供选择的方式来定位特定的建筑物。 第三个属性，`stree`，则用来保存地址中的街道名称的：

```swift
class Address {
    var buildingName: String?
    var buildingNumber: String?
    var street: String?
    func buildingIdentifier() -> String? {
        if buildingName {
            return buildingName
        } else if buildingNumber {
            return buildingNumber
        } else {
            return nil
        }
    }
}
```
`Address`类中还提供了一个名为`buildingIdentifier`的方法，其返回类型为`String?`。 这个方法检查`buildingName`及`buildingName`是否有值，若`buildingName`有值则返回`buildingName`，若非则返回`buildingNumber`的值，如果两者均无则返回空。

##以可选链方式的属性调用

如先前演示的可选链做为强制解析的一个替代方式，你可以利用可选链来访问可选元素的属性，及检测属性的访问是否能成功，但你不能通过可选链的方式为属性赋值。

利用前先写好的类一个新的`Person`实例，并与之前先一样尝试访问它的`numberOfRooms`属性：

```swift
let john = Person()
if let roomCount = john.residence?.numberOfRooms {
    println("John's residence has \(roomCount) room(s).")
} else {
    println("Unable to retrieve the number of rooms.")
}
// 打印 "Unable to retrieve the number of rooms。
```

因为`john.residence`为空，所以这个可选链与先前的一样调用失败并没引错误。

##以可选链方式的方法调用法

你能以可选链的方式去调用一个可选元素的方法，及检测是否方法调用不否成功。即使在方法没有定义返回值的情况下一样可行。

`Residence`的`printNumberOfRooms`方法会打印`numberOfRooms`的当前值。方法如下：

```swift
func printNumberOfRooms(){
	println(“The number of rooms is \(numberOfRooms)”)
}
```
这个方法没有声明返回值，无返回值函数及方法都会带有一个隐式的返回类型为`Void`（参见Function Without Return Values）。

如果你通过可选链的方式去调用一个可选元素的方法，该方法返回的将是`Void?`，而非`Void`，因为通过可选链方式调用的方法返回的均为可选类型。这样让你可以通过一个`If`语句去测试`printNumberOfRooms`方法是否可调用，即使该方法本身没有定义返回值。当`printNumberOfRooms`方法通过可选链调用成功时隐式的返回值为`Void`，否非为空：

```swift
if john.residence?.printNumberOfRooms() {
    println("It was possible to print the number of rooms.")
} else {
    println("It was not possible to print the number of rooms.")
}
// 打印 "It was not possible to print the number of rooms."。
```

##以可选链方式的下标调用

你可以通过可选链的方式去获取可选元素对应下标的值，及判断下标调用是否成功，然而，你不能在可选链中去设置一个下标的值。

> 注意：  
当你要通过可选链的试访问对应可选元素的下标时，你应该将问号置于下标所带的括号前，而非后。可选链的问号通常都是紧随表达式中的可选元素后的。

下面的例子中我们将通过在`Residence`类中定义的下标去获取`rooms`数组中第一间房间的名称。由于`john.residence`当前为空，所以下标的调用失败。

```swift
if let firstRoomName = john.residence?[0].name {
    println("The first room name is \(firstRoomName).")
} else {
    println("Unable to retrieve the first room name.")
}
// 打印 "Unable to retrieve the first room name."。
```

下标调用时我们将可选链的问号置于`john.residence`后于下标的括号前。因为`john.residence`为可选链需要尝试调用的可选元素。

如果我们为`john.residence`创建并分配一个`Residence`实体且其`rooms`属性带一个或多个Room实体，你就可以通过`Residence`的下标在可选链中访问对应的成员了：

```swift
let johnsHouse = Residence()
johnsHouse.rooms += Room(name: "Living Room")
johnsHouse.rooms += Room(name: "Kitchen")
john.residence = johnsHouse

if let firstRoomName = john.residence?[0].name {
    println("The first room name is \(firstRoomName).")
} else {
    println("Unable to retrieve the first room name.")
}
// 打印 "The first room name is Living Room."。
```

##多层链式

你可以通过多层链式来访问实体中的属性，方法及下标。多层可选链式调用并不会增加返回值的可选性/形成可选嵌套。

也就是说：

通过可选链得到的值一定为可选类型，无论你想获取的目标值是否为可选。同理一个目标值原为可选元素，不过因为链式的调用而加深变可选性。

因此：

当你想从可选链中得到一个`Int`时，你得到的总会是一个`Int?`类型的值，无论通过多少层的可选链。相同的，原为`Int?`类型的返回值也一样，无论经过多少层得到的还是`Int?`类型。 

下面的例子中我们将尝试访问从`john`的`residence`属性中的`address`属于获取期其`street`属性的值。这里我们将有两层的可选链调用，链式中的两环`residence`和`address`均为可选类型的属性：

```swift
if let johnsStreet = john.residence?.address?.street {
    println("John's street name is \(johnsStreet).")
} else {
    println("Unable to retrieve the address.")
}
// 打印 "Unable to retrieve the address.”。
```

虽然当前的`john.residence`含有一个有效的`Residence`实例。然而`john.residence.address`的还是为空值，所以调用`john.residence?.address?.street`失败了。

值得注意在下面的例子中，你将尝试去获得`street`属性的值。 这个属性的类型为`String?`。所以`john.residence?.address?`的返回值也是`String?`，即使经过了两层的可选链路来访问。

如果你为`john.street.address`分配一个真实的`Address`实例并为其`street`赋值，你就可以通过多层可用选连的试去访问相关的值。

```swift
let johnsAddress = Address()
johnsAddress.buildingName = "The Larches"
johnsAddress.street = "Laurel Street"
john.residence!.address = johnsAddress
```

```swift
if let johnsStreet = john.residence?.address?.street {
    println("John's street name is \(johnsStreet).")
} else {
    println("Unable to retrieve the address.")
}
// 打印 "John's street name is Laurel Street."。
```

注意我们需要通过感叹号来为`jonh.residence.address`赋值。 因为`john.residence`属性是一个可选类型，所以在为`residence`的`address`属性赋值前，我们需要用感叹得到它的实际值先。

##返回可选值方法的链式调用

先前的例子中我们展示了如果通过可选链路来获取一个可选属性的值。如有需要我们也可以用可选链的方式去调用返回值为可选类型的方法，并也可将其返回值做为链式中的一环。

下下面的例子中通过可选链调用了`Address`类的`buildingIdentifier`方法。 这个方法的返回类型为`String?`。 如先前所述，通过可选链调用该方法的最终返回类型也是为`String?`：

```swift
if let buildingIdentifier = john.residence?.address?.buildingIdentifier() {
    println("John's building identifier is \(buildingIdentifier).")
}
// 打印 "John's building identifier is The Larches."。
```

如果你想将该方法的返回值也置于链式中，只需将可选链路的问号置于方法调用的括号后：

```swift
if let upper = john.residence?.address?.buildingIdentifier()?.uppercaseString {
    println("John's uppercase building identifier is \(upper).")
}
// 打印 "John's uppercase building identifier is THE LARCHES."。
```

> 注意：  
在上面的例子中，你将可选链的问号置于括后面是因为你想加入链式中的可选元素是`buildingIdentifier`的返回值，而不是该方法本身。
