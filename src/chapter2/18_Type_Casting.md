#Type Casting

Type casting is a way to check the type of an instance, and/or to treat that instance as if it is a different superclass or subclass from somewhere else in its own class hierarchy.

Type casting in Swift is implemented with the is and as operators. These two operators provide a simple and expressive way to check the type of a value or cast a value to a different type.

You can also use type casting to check whether a type conforms to a protocol, as described in Checking for Protocol Conformance.

# 类型检查
类型检查的目的是为了检查实例的类型，并且可以用来类型转换，可以让实例找到自己所在的继承树，以及在继承树中上下转换类型。 

类型检查使用`is`和`as`操作符来实现。这两个操作符提供了一种简单明了的方式来进行类型检查和类型转换。 

你还可以使用类型检查来检查类型是否符合接口，以及是否和接口描述保持一致 ,如[Checking for Protocol Conformance](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Protocols.html#//apple_ref/doc/uid/TP40014097-CH25-XID_363)小节所述。

##Defining a Class Hierarchy for Type Casting

You can use type casting with a hierarchy of classes and subclasses to check the type of a particular class instance and to cast that instance to another class within the same hierarchy. The three code snippets below define a hierarchy of classes and an array containing instances of those classes, for use in an example of type casting.

The first snippet defines a new base class called MediaItem. This class provides basic functionality for any kind of item that appears in a digital media library. Specifically, it declares a name property of type String, and an init name initializer. (It is assumed that all media items, including all movies and songs, will have a name.)

## 为类型检查定义一个继承树

你可以使用类型检查来检查一个实例的具体类型，也可以把实例转化为继承树中的另一种类型。下面的三个代码片段定义一个类的继承关系和包含这些类实例的数组，作为类型转换的一个例子使用。 

第一个片段定义了一个名为`MediaItem`的基类。这个类提供数字媒体处理库中其他类的基本功能。具体来说，它声明一个`String`类型的`name`属性，以及一个叫`init`的初始化方法。 （假设所有的媒体项目，包括所有的电影和歌曲，将有一个名称。）

    class MediaItem {
        var name: String
        init(name: String) {
            self.name = name
        }
    }
The next snippet defines two subclasses of MediaItem. The first subclass, Movie, encapsulates additional information about a movie or film. It adds a director property on top of the base MediaItem class, with a corresponding initializer. The second subclass, Song, adds an artist property and initializer on top of the base class:

接下来的代码定义了`MediaItem`的两个子类。第一个子类`Movie`，封装了有关`Movie`的附加信息。它增加了属性`director`及其初始化方法。第二个子类`Song`，增加了属性`artist`及其初始化方法：

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

最后的代码创建一个常量数组`library`，其中包含两个`Movie`实例和三首`Song`的实例。`library`数组的类型是由它里面包含的内容决定的。Swift能够识别出`Movie`和`Song`有MediaItem一个共同的父类，所以它会推断出`library`是一个`MediaItem[] `类型的数组。

    let library = [
        Movie(name: "Casablanca", director: "Michael Curtiz"),
        Song(name: "Blue Suede Shoes", artist: "Elvis Presley"),
        Movie(name: "Citizen Kane", director: "Orson Welles"),
        Song(name: "The One And Only", artist: "Chesney Hawkes"),
        Song(name: "Never Gonna Give You Up", artist: "Rick Astley")
    ]
    // the type of "library" is inferred to be MediaItem[]
The items stored in library are still Movie and Song instances behind the scenes. However, if you iterate over the contents of this array, the items you receive back are typed as MediaItem, and not as Movie or Song. In order to work with them as their native type, you need to check their type, or downcast them to a different type, as described below.

`library`中的子元素仍然是`Movie`或`Song`的实例。但是，如果你遍历这个数组，返回的是`MediaItem`类型的实例，而不是`Movie`或`Song`。为了使用他们自身的类型，你需要检查它们的类型，或将它们向下转换为不同的类型，如下所述。

##Checking Type

Use the type check operator (is) to check whether an instance is of a certain subclass type. The type check operator returns true if the instance is of that subclass type and false if it is not.

The example below defines two variables, movieCount and songCount, which count the number of Movie and Song instances in the library array:

## 检查类型 

使用类型检查运算符（`is`）来检查一个实例是否是一个类的子类。如果是，则返回`true`，否则返回`false`。

下面的例子定义了两个变量，`movieCount`和`songCount`，用来统计数组中`Movie` 和`Song` 的数量。

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
    // 打印出 "Media library 包含 2 movies and 3 songs"
    
This example iterates through all items in the library array. On each pass, the for-in loop sets the item constant to the next MediaItem in the array.

item is Movie returns true if the current MediaItem is a Movie instance and false if it is not. Similarly, item is Song checks whether the item is a Song instance. At the end of the for-in loop, the values of movieCount and songCount contain a count of how many MediaItem instances were found of each type.

这个例子遍历了数组中的所有元素，每一次循环，都会把数组中的一个实例赋值给`item`。 

如果`item`是`Movie`类型，则返回 `true`否则返回`false`。同样，也会检查`item`是否是`Song`类型。最后，`movieCount`和`songCount`即为每个类型的实例数。


##Downcasting

A constant or variable of a certain class type may actually refer to an instance of a subclass behind the scenes. Where you believe this is the case, you can try to downcast to the subclass type with the type cast operator (as).

Because downcasting can fail, the type cast operator comes in two different forms. The optional form, as?, returns an optional value of the type you are trying to downcast to. The forced form, as, attempts the downcast and force-unwraps the result as a single compound action.

## 向下转型
有时候，一些实例的类型是它父类的类型，这个时候你就需要使用`as`操作符进行向下转型。

因为向下转型可能会失败，类型转换操作符带有两种不同形式。可选形式（ optional form）` as? `返回一个你试图下转成的类型的可选值（optional value）。强制形式 `as` 则会先向下转型并把转型结果强制解包（force-unwraps）。

Use the optional form of the type cast operator (as?) when you are not sure if the downcast will succeed. This form of the operator will always return an optional value, and the value will be nil if the downcast was not possible. This enables you to check for a successful downcast.

Use the forced form of the type cast operator (as) only when you are sure that the downcast will always succeed. This form of the operator will trigger a runtime error if you try to downcast to an incorrect class type.

当你不确定向下转型能否成功时，使用`as?`，转型失败时返回`nil `。这样你就能判断是否转型成功。

当你对类型确定的对象进行向下转型时，使用`as`，转型失败就会抛错。

The example below iterates over each MediaItem in library, and prints an appropriate description for each item. To do this, it needs to access each item as a true Movie or Song, and not just as a MediaItem. This is necessary in order for it to be able to access the director or artist property of a Movie or Song for use in the description.

In this example, each item in the array might be a Movie, or it might be a Song. You don’t know in advance which actual class to use for each item, and so it is appropriate to use the optional form of the type cast operator (as?) to check the downcast each time through the loop:

如下例，我们的目的是遍历`library`里的每一个` MediaItem` ，并打印出正确的描述信息。为了达到这个目的，`item`需要真正作为`Movie` 或 `Song`的类型来使用，而非仅仅是 `MediaItem`。因为我们在打印描述信息时，必须要用到`Movie`的`director`属性或 `Song`的`artist`属性。

数组中的每一个`item`可能是 `Movie` 或 `Song`。 事先你不知道每个`item`的真实类型，所以使用可选形式的类型转换 (`as?`)去检查每次向下转型。

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

示例中，因为 `item` 是一个 `MediaItem` 类型的实例，它可能是一个`Movie`，所以我们首先试图将 `item` 下转为 `Movie`。同样，它也可能是一个 `Song`，或者仅仅是基类 `MediaItem`。所以，`as?`形式试图下转时返还一个可选值。 `item as Movie` 的返回值是`Movie?`类型或 “optional Movie”。

Downcasting to Movie fails when applied to the two Song instances in the library array. To cope with this, the example above uses optional binding to check whether the optional Movie actually contains a value (that is, to find out whether the downcast succeeded.) This optional binding is written “if let movie = item as? Movie”, which can be read as:

“Try to access item as a Movie. If this is successful, set a new temporary constant called movie to the value stored in the returned optional Movie.”

把数组`library`中的两个`Song`对象进行向下转型为`Movie`时，会转型失败。所以，使用临时赋值来检查是否转型成功。临时赋值的写法是`if let movie = item as? Movie`，意思就是“尝试把`item`转型为`Movie`，如果转型成功，则把转化后的对象存储在临时变量`movie`中“。

If the downcasting succeeds, the properties of movie are then used to print a description for that Movie instance, including the name of its director. A similar principle is used to check for Song instances, and to print an appropriate description (including artist name) whenever a Song is found in the library.

如果向下转型成功，则会打印`Movie`对象相关的属性，包括导演的姓名，同样，如果`Song`转型成功，也会打印出`Song`相关的属性，例如歌手的姓名。

> NOTE

> Casting does not actually modify the instance or change its values. The underlying instance remains the same; it is >simply treated and accessed as an instance of the type to which it has been cast.
 
>注意 

>实际上，类型转换并没有对实例进行修改，只是使用时，被当作一种类型来处理和访问。

##Type Casting for Any and AnyObject

Swift provides two special type aliases for working with non-specific types:

AnyObject can represent an instance of any class type.
Any can represent an instance of any type at all, apart from function types.
NOTE

Use Any and AnyObject only when you explicitly need the behavior and capabilities they provide. It is always better to be specific about the types you expect to work with in your code.


## Any和AnyObject 的类型转换

`Swift` 提供了两种特殊类型，用来表示非特定类型。

`AnyObject`表示任何类类型的实例。 
`Any` 表示任何类型的实例，函数类型除外。 

注意：
只有当你确定需要使用`Any`和`AnyObject`的特性的时候，再使用它们。一般情况下，最好还是指定具体的类型。
###AnyObject

When working with Cocoa APIs, it is common to receive an array with a type of AnyObject[], or “an array of values of any object type”. This is because Objective-C does not have explicitly typed arrays. However, you can often be confident about the type of objects contained in such an array just from the information you know about the API that provided the array.

### AnyObject 
使用Cocoa APIs时，返回值为AnyObject类型的数组很常见。这是因为Objective-C 没有确定类型的数组。尽管如此，如果对具体API熟悉的话，你仍然可以放心的使用这个API。

In these situations, you can use the forced version of the type cast operator (as) to downcast each item in the array to a more specific class type than AnyObject, without the need for optional unwrapping.

The example below defines an array of type AnyObject[] and populates this array with three instances of the Movie class:


在这些情况下，您可以使用as 把AnyObject转化为一个具体的类型，而不需要进行拆包。

下面的例子定义了一个类型为AnyObject[]的数组，包含三个Movie类型的对象。

    let someObjects: AnyObject[] = [
        Movie(name: "2001: A Space Odyssey", director: "Stanley Kubrick"),
        Movie(name: "Moon", director: "Duncan Jones"),
        Movie(name: "Alien", director: "Ridley Scott")
    ]
    
Because this array is known to contain only Movie instances, you can downcast and unwrap directly to a non-optional Movie with the forced version of the type cast operator (as):

因为你已经知道这个数组中全都是Movie类型的对象，所以你可以直接使用as进行向下转型：

    for object in someObjects {
        let movie = object as Movie
        println("Movie: '\(movie.name)', dir. \(movie.director)")
    }
    // Movie: '2001: A Space Odyssey', dir. Stanley Kubrick
    // Movie: 'Moon', dir. Duncan Jones
    // Movie: 'Alien', dir. Ridley Scott
For an even shorter form of this loop, downcast the someObjects array to a type of Movie[] instead of downcasting each item:

上面的代码可以简写，你可以直接把数组转型而不用对数组中的每一个对象转型。

    for movie in someObjects as Movie[] {
        println("Movie: '\(movie.name)', dir. \(movie.director)")
    }
    // Movie: '2001: A Space Odyssey', dir. Stanley Kubrick
    // Movie: 'Moon', dir. Duncan Jones
    // Movie: 'Alien', dir. Ridley Scott

### Any

Here’s an example of using Any to work with a mix of different types, including non-class types. The example creates an array called things, which can store values of type Any:

### Any

下面的例子中，使用了`Any`来处理包含了多种混合类型，甚至一些非类类型的场景。在这个例子中，我们创建了一个`things`数组用来存储任何类型的元素。

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

`things`数组包含两个`int`值，两个`Double`值，一个字符串值，一个元组，和一个Movie对象。 

你可以在`switch`语句中使用`is`和`as`操作符来确定数组中`Any`和`AnyObject`变量的的具体类型。如下遍历数组`things`中的每一个元素，并确定他们的类型。为了打印元素的值，一些`switch` 语句把元素赋值给一个指定的类型。

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

> 这个示例使用 `as` 而不是 `as?` 来进行类型转换，因为在`switch`上下文中，类型检查是安全的。
