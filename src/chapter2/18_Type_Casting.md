#Type Casting

Type casting is a way to check the type of an instance, and/or to treat that instance as if it is a different superclass or subclass from somewhere else in its own class hierarchy.

Type casting in Swift is implemented with the is and as operators. These two operators provide a simple and expressive way to check the type of a value or cast a value to a different type.

You can also use type casting to check whether a type conforms to a protocol, as described in Checking for Protocol Conformance.

# 类型转换
类型转换是一种方法来检查一个实例的类型，和/或处理该实例，就好像它是一个不同的超类或子类从别的在自己的类层次结构中的某个地方。 

类型转换使用is和as操作符来实现。这两个操作符提供了一种简单和富有表现力的方法来检查一个值的类型或把某个值转换为不同的类型。 
你还可以使用类型转换来检查类型是否符合，如在检查协议一致性描述。

##Defining a Class Hierarchy for Type Casting

You can use type casting with a hierarchy of classes and subclasses to check the type of a particular class instance and to cast that instance to another class within the same hierarchy. The three code snippets below define a hierarchy of classes and an array containing instances of those classes, for use in an example of type casting.

The first snippet defines a new base class called MediaItem. This class provides basic functionality for any kind of item that appears in a digital media library. Specifically, it declares a name property of type String, and an init name initializer. (It is assumed that all media items, including all movies and songs, will have a name.)

## 定义一个类继承为类型转换

您可以使用类型转换与类和子类的层次结构来检查一个特定的类实例的类型和投该实例到另一个类中的同一层级内。下面的三个代码片段定义的类层次结构和包含这些类的实例数组，用于类型转换的一个例子使用。 

第一个片段定义了一个名为MediaItem新的基类。这个类提供基本功能，任何类型的项目出现在一个数字媒体库。具体来说，它声明一个String类型的name属性，以及一个init名称初始值设定项。 （假设所有的媒体项目，包括所有的电影和歌曲，将有一个名称。）

    class MediaItem {
        var name: String
        init(name: String) {
            self.name = name
        }
    }
The next snippet defines two subclasses of MediaItem. The first subclass, Movie, encapsulates additional information about a movie or film. It adds a director property on top of the base MediaItem class, with a corresponding initializer. The second subclass, Song, adds an artist property and initializer on top of the base class:

接下来的片断定义MediaItem的两个子类。第一个子类，电影，封装了有关电影或电影的附加信息。它增加了一个属性主任在基MediaItem类的顶部，有一个相应的初始化。第二个亚类，宋，增加了一个艺术家财产和初始化基类的顶部：

    class Movie: MediaItem {
        var director: String
        init(name: String, director: String) {
            self.director = director
            super.init(name: name)
        }
    }
     
    class Song: MediaItem {
        var artist: String
        init(name: String, artist: String) {
            self.artist = artist
            super.init(name: name)
        }
    }
The final snippet creates a constant array called library, which contains two Movie instances and three Song instances. The type of the library array is inferred by initializing it with the contents of an array literal. Swift’s type checker is able to deduce that Movie and Song have a common superclass of MediaItem, and so it infers a type of MediaItem[] for the library array:

最后的代码片断创建一个常量数组叫做库，其中包含两个电影实例和三首歌曲的实例。图书馆数组的类型是由具有数组文本的内容初始化它的推断。斯威夫特的类型检查是能够演绎出电影和歌曲有MediaItem一个共同的超类，所以它会推断图书馆数组类型MediaItem[]中：

    let library = [
        Movie(name: "Casablanca", director: "Michael Curtiz"),
        Song(name: "Blue Suede Shoes", artist: "Elvis Presley"),
        Movie(name: "Citizen Kane", director: "Orson Welles"),
        Song(name: "The One And Only", artist: "Chesney Hawkes"),
        Song(name: "Never Gonna Give You Up", artist: "Rick Astley")
    ]
    // the type of "library" is inferred to be MediaItem[]
The items stored in library are still Movie and Song instances behind the scenes. However, if you iterate over the contents of this array, the items you receive back are typed as MediaItem, and not as Movie or Song. In order to work with them as their native type, you need to check their type, or downcast them to a different type, as described below.

存储在库中的项目仍然在幕后电影和歌曲实例。但是，如果你遍历这个数组的内容，您会收到回项目类型为MediaItem，而不是电影或歌曲。为了与他们合作，因为他们自身的类型，你需要检查它们的类型，或将它们向下转换为不同的类型，如下所述。

##Checking Type

Use the type check operator (is) to check whether an instance is of a certain subclass type. The type check operator returns true if the instance is of that subclass type and false if it is not.

The example below defines two variables, movieCount and songCount, which count the number of Movie and Song instances in the library array:

## 检查类型 

使用类型检查运算符（是）来检查一个实例是否是一个子类的类型。如果实例是子类的类型和虚假的，如果它不是类型检查运算符返回true。 

下面的例子定义了两个变量，movieCount和songCount，这算电影和歌曲实例库中的数组数：

    var movieCount = 0
    var songCount = 0
     
    for item in library {
        if item is Movie {
            ++movieCount
        } else if item is Song {
            ++songCount
        }
    }
     
    println("Media library contains \(movieCount) movies and \(songCount) songs")
    // prints "Media library contains 2 movies and 3 songs"
    
This example iterates through all items in the library array. On each pass, the for-in loop sets the item constant to the next MediaItem in the array.

item is Movie returns true if the current MediaItem is a Movie instance and false if it is not. Similarly, item is Song checks whether the item is a Song instance. At the end of the for-in loop, the values of movieCount and songCount contain a count of how many MediaItem instances were found of each type.

通过图书馆阵列中的所有项目本示例循环。在每个传中，for-in循环设置项常量数组中的下一个MediaItem。 

产品如果当前MediaItem是一个Movie实例和虚假的，如果它不是电影返回true。同样，产品松检查项目是否为宋实例。在for-in循环的结束，movieCount和songCount的值包含多少MediaItem实例中发现每种类型的计数。

##Downcasting

A constant or variable of a certain class type may actually refer to an instance of a subclass behind the scenes. Where you believe this is the case, you can try to downcast to the subclass type with the type cast operator (as).

Because downcasting can fail, the type cast operator comes in two different forms. The optional form, as?, returns an optional value of the type you are trying to downcast to. The forced form, as, attempts the downcast and force-unwraps the result as a single compound action.

## 向下转换 

某一类类型的常量或变量可能实际上是指在幕后一个子类的实例。在那里你认为是这样的话，你可以尝试向下转换与类型转换运算符（如）的子类型。 

因为向下转换可能会失败，类型转换运算符有两种不同的形式。可选的形式，？，返回你试图向下转换到该类型的可选值。强制的形式，如，试图丧气和强制解开的结果作为一个单一的复合动作。

Use the optional form of the type cast operator (as?) when you are not sure if the downcast will succeed. This form of the operator will always return an optional value, and the value will be nil if the downcast was not possible. This enables you to check for a successful downcast.

Use the forced form of the type cast operator (as) only when you are sure that the downcast will always succeed. This form of the operator will trigger a runtime error if you try to downcast to an incorrect class type.

使用类型转换运算符的可选形式（as？）时，你是不知道，如果向下转换会成功。这种形式的运算符将始终返回一个可选值，该值将为零，如果向下转换是不可能的。这使您可以检查是否有成功的垂头丧气。 

使用类型转换运算符的强制形式（如）只有当你确定低垂将始终成功。如果您尝试向下转换到一个不正确的类类型这种形式的操作会触发一个运行时错误。

The example below iterates over each MediaItem in library, and prints an appropriate description for each item. To do this, it needs to access each item as a true Movie or Song, and not just as a MediaItem. This is necessary in order for it to be able to access the director or artist property of a Movie or Song for use in the description.

In this example, each item in the array might be a Movie, or it might be a Song. You don’t know in advance which actual class to use for each item, and so it is appropriate to use the optional form of the type cast operator (as?) to check the downcast each time through the loop:

下面遍历每个MediaItem库，并打印每个项目的适当描述的例子。要做到这一点，它需要访问每个项目作为一个真正的电影或歌曲，而不是仅仅作为一个MediaItem。这是必要的，以便它能够访问一个电影或歌曲的导演或艺人属性在描述中使用。 

在这个例子中，数组中的每个项目可能是电影，也可能是一首乐曲。你不事先知道哪一个实际的类使用的每个项目，所以它是适合使用类型转换运算符的可选形式（如？）通过每次循环检查垂头丧气：

    for item in library {
        if let movie = item as? Movie {
            println("Movie: '\(movie.name)', dir. \(movie.director)")
        } else if let song = item as? Song {
            println("Song: '\(song.name)', by \(song.artist)")
        }
    }
     
    // Movie: 'Casablanca', dir. Michael Curtiz
    // Song: 'Blue Suede Shoes', by Elvis Presley
    // Movie: 'Citizen Kane', dir. Orson Welles
    // Song: 'The One And Only', by Chesney Hawkes
    // Song: 'Never Gonna Give You Up', by Rick Astley
The example starts by trying to downcast the current item as a Movie. Because item is a MediaItem instance, it’s possible that it might be a Movie; equally, it’s also possible that it might a Song, or even just a base MediaItem. Because of this uncertainty, the as? form of the type cast operator returns an optional value when attempting to downcast to a subclass type. The result of item as Movie is of type Movie?, or “optional Movie”.

这个例子开始试图通过向下转换当前项目作为电影。因为项目是一个MediaItem例如，它是可能的，它可能是一个电影;同样，它也有可能是它可能的乐曲，甚至只是一个基础MediaItem。由于这种不确定性，将作为？试图向下转换到子类类型时，类型转换运算符的形式返回一个可选值。项目作为电影的结果是类型的电影？，或“可选的电影”。

Downcasting to Movie fails when applied to the two Song instances in the library array. To cope with this, the example above uses optional binding to check whether the optional Movie actually contains a value (that is, to find out whether the downcast succeeded.) This optional binding is written “if let movie = item as? Movie”, which can be read as:

当在库阵列施加到两个乐曲实例向下转换到电影失败。为了解决这个问题，上面的示例使用可选的绑定检查可选电影实际上是否包含一个值（也就是要找出垂头丧气是否成功。）这个可选的结合上记着说“如果让电影=项目作为？电影“，这可以被理解为：

“Try to access item as a Movie. If this is successful, set a new temporary constant called movie to the value stored in the returned optional Movie.”

“尝试访问项目作为一个电影。如果这是成功，树立了新的临时常数，称为电影存储在返回的可选电影的价值。“ 

If the downcasting succeeds, the properties of movie are then used to print a description for that Movie instance, including the name of its director. A similar principle is used to check for Song instances, and to print an appropriate description (including artist name) whenever a Song is found in the library.

如果向下转型成功，电影的属性，然后用于打印的Movie实例说明，包括其导演的名字。类似的原理是用来检查宋实例，并打印相应的描述（包括艺术家的名字），每当乐曲库中找到。

> NOTE

> Casting does not actually modify the instance or change its values. The underlying instance remains the same; it is >simply treated and accessed as an instance of the type to which it has been cast.
 
 
 >注意 

>铸造实际上并不修改实例或改变其值。相关实例保持不变;它是>简单的处理，并作为访问到它已被转换到的类型的一个实例。

##Type Casting for Any and AnyObject

Swift provides two special type aliases for working with non-specific types:

AnyObject can represent an instance of any class type.
Any can represent an instance of any type at all, apart from function types.
NOTE

Use Any and AnyObject only when you explicitly need the behavior and capabilities they provide. It is always better to be specific about the types you expect to work with in your code.


## 类型转换为任何和AnyObject 

swift 提供了两种特殊类型的别名与非特定类型的工作： 

AnyObject可以代表任何类类型的实例。 
任何可以代表任何类型的实例可言，除了函数类型。 
注 

使用任何与AnyObject只有当你明确需要他们提供的行为和能力。它始终是更好地具体说明你希望在你的代码工作的类型。

###AnyObject

When working with Cocoa APIs, it is common to receive an array with a type of AnyObject[], or “an array of values of any object type”. This is because Objective-C does not have explicitly typed arrays. However, you can often be confident about the type of objects contained in such an array just from the information you know about the API that provided the array.

### AnyObject 

当Cocoa API的工作，是很常见的接收数组与一类AnyObject[]，或者“任何对象类型的值的数组”。这是因为Objective-C中没有显式类型的数组。但是，你常常可以充满信心包含在刚刚从你了解所提供的数组的API的信息，例如一个数组对象的类型。

In these situations, you can use the forced version of the type cast operator (as) to downcast each item in the array to a more specific class type than AnyObject, without the need for optional unwrapping.

The example below defines an array of type AnyObject[] and populates this array with three instances of the Movie class:

在这些情况下，您可以使用类型转换运算符的强迫版本（如）向下转换到每个项目在数组中以一个更具体的类类型比AnyObject，而不需要选配解缠。 

下面的例子定义类型AnyObject[]数组，并填充这个数组的Movie类的三个实例：

    let someObjects: AnyObject[] = [
        Movie(name: "2001: A Space Odyssey", director: "Stanley Kubrick"),
        Movie(name: "Moon", director: "Duncan Jones"),
        Movie(name: "Alien", director: "Ridley Scott")
    ]
    
Because this array is known to contain only Movie instances, you can downcast and unwrap directly to a non-optional Movie with the forced version of the type cast operator (as):

因为这个数组是已知含有唯一的电影实例，则可以向下转换，直接解开到一个非可选的电影与类型转换运算符（如）的强迫版本：

    for object in someObjects {
        let movie = object as Movie
        println("Movie: '\(movie.name)', dir. \(movie.director)")
    }
    // Movie: '2001: A Space Odyssey', dir. Stanley Kubrick
    // Movie: 'Moon', dir. Duncan Jones
    // Movie: 'Alien', dir. Ridley Scott
For an even shorter form of this loop, downcast the someObjects array to a type of Movie[] instead of downcasting each item:

对于这个循环的一个更短的形式，向下转型的someObjects阵列的类型电影[]的，而不是向下转换每个项目：

    for movie in someObjects as Movie[] {
        println("Movie: '\(movie.name)', dir. \(movie.director)")
    }
    // Movie: '2001: A Space Odyssey', dir. Stanley Kubrick
    // Movie: 'Moon', dir. Duncan Jones
    // Movie: 'Alien', dir. Ridley Scott

### Any

Here’s an example of using Any to work with a mix of different types, including non-class types. The example creates an array called things, which can store values of type Any:

### Any

下面是使用Any与混合不同类型的，包括非类类型的工作的一个例子。该示例创建一个名为事情一个数组，它可以存储任何类型的值：

    var things = Any[]()
     
    things.append(0)
    things.append(0.0)
    things.append(42)
    things.append(3.14159)
    things.append("hello")
    things.append((3.0, 5.0))
    things.append(Movie(name: "Ghostbusters", director: "Ivan Reitman"))


The things array contains two Int values, two Double values, a String value, a tuple of type (Double, Double), and the movie “Ghostbusters”, directed by Ivan Reitman.

You can use the is and as operators in a switch statement’s cases to discover the specific type of a constant or variable that is known only to be of type Any or AnyObject. The example below iterates over the items in the things array and queries the type of each item with a switch statement. Several of the switch statement’s cases bind their matched value to a constant of the specified type to enable its value to be printed:

事情数组包含两个int值，两个Double值，一个字符串值，类型（Double，Double）的一个元组，和电影“捉鬼敢死队”，导演伊万·瑞特曼。 

您可以使用is和as在switch语句的情况下，运营商发现，只知道是任何类型或AnyObject的常量或变量的具体类型。下面迭代的事情阵列项目的例子，查询每个项目的用switch语句的类型。几个switch语句的情况下，其匹配的值绑定到指定的类型，使其值要打印的常数：

    for thing in things {
        switch thing {
        case 0 as Int:
            println("zero as an Int")
        case 0 as Double:
            println("zero as a Double")
        case let someInt as Int:
            println("an integer value of \(someInt)")
        case let someDouble as Double where someDouble > 0:
            println("a positive double value of \(someDouble)")
        case is Double:
            println("some other double value that I don't want to print")
        case let someString as String:
            println("a string value of \"\(someString)\"")
        case let (x, y) as (Double, Double):
            println("an (x, y) point at \(x), \(y)")
        case let movie as Movie:
            println("a movie called '\(movie.name)', dir. \(movie.director)")
        default:
            println("something else")
        }
    }
    
    // zero as an Int
    // zero as a Double
    // an integer value of 42
    // a positive double value of 3.14159
    // a string value of "hello"
    // an (x, y) point at 3.0, 5.0
    // a movie called 'Ghostbusters', dir. Ivan Reitman
>NOTE

>The cases of a switch statement use the forced version of the type cast operator (as, not as?) to check and cast to a >specific type. This check is always safe within the context of a switch case statement.

>注意 

> switch语句的情况下使用的类型转换运算符的强迫版本（作为，不作为？）检查并转换成一个>特定类型。这种检查始终是一个安全的switch case语句的上下文中。
