# 析构过程 (Deinitialization)

A deinitializer is called immediately before a class instance is deallocated. You write deinitializers with the deinit keyword, similar to how intializers are written with the init keyword. Deinitializers are only available on class types.”

> 析构函数会在一个类的实例被释放之前被立即调用。用`deinit`关键词来声明析构函数，就像使用`init`来标示初始化的函数一样，只有在类中才存在析构函数。

#### How Deinitialization Works

> ####  析构过程是如何工作的

Swift automatically deallocates your instances when they are no longer needed, to free up resources. Swift handles the memory management of instances through automatic reference counting (ARC), as described in Automatic Reference Counting. Typically you don’t need to perform manual clean-up when your instances are deallocated. However, when you are working with your own resources, you might need to perform some additional clean-up yourself. For example, if you create a custom class to open a file and write some data to it, you might need to close the file before the class instance is deallocated.

> Swift 会自动释放不再需要的实例以释放资源。如自动引用计数那一章描述，Swift 通过[自动引用计数（ARC）](http://siemenliu.gitbooks.io/the-swift-programming-language-in-chinese/src/chapter2/16_Automatic_Reference_Counting.html)处理实例的内存管理。通常当你的实例被释放时不需要手动地去清理。但对于占用中的资源，你可能需要做一些额外的清理工作。例如，如果创建了一个自定义的类来打开一个文件，并写入一些数据，你可能需要在类实例被释放之前关闭该文件。


Class definitions can have at most one deinitializer per class. The deinitializer does not take any parameters and is written without parentheses:

> 在类的定义中，每个类最多只能有一个析构函数。析构函数不带任何参数，在写法上不带括号：

````
deinit {
    // 执行析构过程
}
````


Deinitializers are called automatically, just before instance deallocation takes place. You are not allowed to call a deinitializer yourself. Superclass deinitializers are inherited by their subclasses, and the superclass deinitializer is called automatically at the end of a subclass deinitializer implementation. Superclass deinitializers are always called, even if a subclass does not provide its own deinitializer.


> 析构函数会自动在实例释放之前被调用，且不支持手动调用。子类会继承父类的析构函数，在子类析构函数执行完之后，将自动调用父类的析构函数。即便子类没有提供自身的析构函数，其父类的析构函数也会被调用。


Because an instance is not deallocated until after its deinitializer is called, a deinitializer can access all properties of the instance it is called on and can modify its behavior based on those properties (such as looking up the name of a file that needs to be closed).

> 因为实例直到实例的析构函数被调用时才会被释放，所以析构函数有权访问所有被调用实例的属性，同时根据那些属性修改其行为（例如查找一个需被关闭文件的名称）。



#### Deinitializers in Action

> #### 析构函数操作


Here’s an example of a deinitializer in action. This example defines two new types, Bank and Player, for a simple game. The Bank structure manages a made-up currency, which can never have more than 10,000 coins in circulation. There can only ever be one Bank in the game, and so the Bank is implemented as a structure with static properties and methods to store and manage its current state:”

> 下面是一个析构函数操作的例子。它是一个简单的游戏，定义了两种新类型，Bank和Player。Bank结构管理一个虚拟硬币的流通，但是它不能拥有超过10,000单位的硬币。游戏中只能有一个Bank存在，所以使用带有静态属性和静态方法的结构的方式来实现Bank，用于储存和管理其当前状态。


````
struct Bank {
    static var coinsInBank = 10_000
    static func vendCoins(var numberOfCoinsToVend: Int) -> Int {
        numberOfCoinsToVend = min(numberOfCoinsToVend, coinsInBank)
        coinsInBank -= numberOfCoinsToVend
        return numberOfCoinsToVend
    }
    static func receiveCoins(coins: Int) {
        coinsInBank += coins
    }
}
````


Bank keeps track of the current number of coins it holds with its coinsInBank property. It also offers two methods—vendCoins and receiveCoins—to handle the distribution and collection of coins.

> Bank根据它的coinsInBank属性来侦听当前存有的硬币数。除此之外Bank还提供两个其它方法，分别是receiveCoins和vendCoins，用于处理硬币的存取。



vendCoins checks that there are enough coins in the bank before distributing them. If there are not enough coins, Bank returns a smaller number than the number that was requested (and returns zero if no coins are left in the bank). vendCoins declares numberOfCoinsToVend as a variable parameter, so that the number can be modified within the method’s body without the need to declare a new variable. It returns an integer value to indicate the actual number of coins that were provided.

> vendCoins方法在 bank 取出硬币之前检查是否有足够的量。如果硬币不足，Bank则返回全部存量(如果硬币量为空则返回 0)。vendCoins方法中将numberOfCoinsToVend声明为一个变量参数，这样就可以在其它方法中对它进行修改，而无需定义一个新的变量。最终vendCoins方法将为取出的硬币返回一个整型值。



The receiveCoins method simply adds the received number of coins back into the bank’s coin store.

> 而 receiveCoins 方法更加简单， 将 bank 的硬币存量和接收到的硬币量相加后再保存回 bank 的硬币存量。



The Player class describes a player in the game. Each player has a certain number of coins stored in their purse at any time. This is represented by the player’s coinsInPurse property:

> 这里Player类定义了游戏中的一个玩家。随时都可能会有若干数量的硬币存入每一个玩家的钱包中。通过 player 的coinsInPurse 属性可以看到这一值：



````
class Player {
    var coinsInPurse: Int
    init(coins: Int) {
        coinsInPurse = Bank.vendCoins(coins)
    }
    func winCoins(coins: Int) {
        coinsInPurse += Bank.vendCoins(coins)
    }
    deinit {
        Bank.receiveCoins(coinsInPurse)
    }
}
````

Each Player instance is initialized with a starting allowance of a specified number of coins from the bank during initialization, although a Player instance may receive fewer than that number if not enough coins are available.

> 每一个Player都由一个初始化函数加上指定硬币量入参实例化得到，他们将在初始化的过程中从 bank 获得硬币。如果 Bank 没有足够的硬币存量用于支付，Player 取得的硬币量可能会比指定的少。



The Player class defines a winCoins method, which retrieves a certain number of coins from the bank and adds them to the player’s purse. The Player class also implements a deinitializer, which is called just before a Player instance is deallocated. Here, the deinitializer simply returns all of the player’s coins to the bank:

> Player类还定义了一个winCoins的方法，该方法可以让player从bank赢取一定数量的硬币存入自己钱包。同时Player类还实现了一个析构函数，它在Player实例释放前一步会被调用。这里的析构函数很简单：将所有player的硬币都返还给银行：




````
var playerOne: Player? = Player(coins: 100)
println("A new player has joined the game with \(playerOne!.coinsInPurse) coins")
// 打印 "新玩家加入游戏，为其分配100硬币"
println("There are now \(Bank.coinsInBank) coins left in the bank")
// 打印 "目前银行硬币存量为： 9900"
````


A new Player instance is created, with a request for 100 coins if they are available. This Player instance is stored in an optional Playedr variable called playerOne. An optional variable is used here, because players can leave the game at any point. The optional lets you track whether there is currently a player in the game.

> 这里创建了一个新的Player实例，如果银行存量充足他将获取100硬币。由于玩家可能随时离开游戏，所以将Player实例存储在一个名为playerOne的可选Player变量中。这样您可以侦听当前是否还有玩家在游戏中。





Because playerOne is an optional, it is qualified with an exclamation mark (!) when its coinsInPurse property is accessed to print its default number of coins, and whenever its winCoins method is called:

> 因为playerOne是可选的，所以由一个感叹号（!）来作前缀，每当其winCoins方法被调用时，会访问其coinsInPurse属性并打印出他的硬币数目。





````
playerOne!.winCoins(2_000)
println("PlayerOne won 2000 coins & now has \(playerOne!.coinsInPurse) coins")
// 打印 "PlayerOne 赢取 2000 硬币，目前他拥有 2100 个硬币"
println("The bank now only has \(Bank.coinsInBank) coins left")
// 打印 "目前银行硬币存量为： 7900"
````




Here, the player has won 2,000 coins. The player’s purse now contains 2,100 coins, and the bank has only 7,900 coins left.

> 以上代码运行后，player 赢取了 2,000 硬币。他的钱包目前有 2,100 个硬币，bank 剩余 7,900 个硬币。



````
playerOne = nil
println("PlayerOne has left the game")
// 打印 "PlayerOne 离开了游戏"
println("The bank now has \(Bank.coinsInBank) coins")
// 打印 "目前银行硬币存量为： 10000"
````


The player has now left the game. This is indicated by setting the optional playerOne variable to nil, meaning “no Player instance.” At the point that this happens, the playerOne variable’s reference to the Player instance is broken. No other properties or variables are still referring to the Player instance, and so it is deallocated in order to free up its memory. Just before this happens, its deinitializer is called automatically, and its coins are returned to the bank.

> 现在player要离开这个游戏。这将把可选的playerOne变量设置为nil，可以理解为“没有Player实例”的意思。这时playerOne变量对Player实例的引用断开。再没有其它属性或者变量还会引用player实例，为了清空内存，它将被释放掉。析构函数会在这一切发生前自动被触发调用，之后所有的硬币将回归到银行，这还真是个游戏。

