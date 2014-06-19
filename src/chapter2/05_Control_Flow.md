# 控制流(Control Flow)

## by moxin.xt

Swift提供类似C语言的控制流语法，比如```for```和```while```循环;```if```和```switch```的条件判断表达式以及``` break```,```continue```这种跳出循环的语句。

Swift除了支持类似C语言这种```for-condition-increment```的表达式外，还支持```for-in```这种循环语句，可以轻松的遍历数组，字典，字符串等序列。

Swift的```switch```语句和C语言相比很强大，它不会像C语言那样，因为在case的分支中忘记写break而执行了下一条case的语句。同时case语句可以匹配任何类型模式，包括区间蒲培，元组和特定类型描述。


#For循环

```for```循环可以将一段代码执行若干次。Swift提供两种```for```循环：

* ```for-in```遍历并返回序列或集合中的每一个元素，执行一段代码
* ```for-condition-increment```在符合某种条件下（通常是在每次循环结束时对计数器+1），返回序列或集合中的每一个元素，执行一段代码。

##For-In

你可以使用```for-in```来遍历集合里的元素;一定范围内的数字;数组中的元素或者字符串中的字符。下面这个例子可以打印出一个5次循环的结果：

```
for index in 1...5{
	println("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25

```

我们首先通过(```...```)表达式创建了一个数字集合，然后枚举集合中的每个元素，```index```值首先被赋值为range(```1```),然后执行循环体内的代码,上面这个例子中循环体内只有一行代码，作用是打印出```index```的值。当这行代码执行完后，```index```值会被更新，被赋值为range(```2```),```println```再次被调用，如此反复，直到循环结束。

上面例子中```index```是个常量，在每次循环开始的时候会被自动赋值，因此它不需要在使用前通过```let```声明，因为它会被```for-in```隐式声明。

	注意
	
	常量```index```的作用域只存在于循环体内。如果你想在循环体外查看```index```的值或者使用它
	你需要在循环开始前声明它。

如果你在遍历某个集合时并不关心集合中的元素，你可以通过下划线来代替集合中的元素变量名：

```
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
println("\(base) to the power of \(power) is \(answer)")
// prints "3 to the power of 10 is 59049”
```
这个例子用来计算某个数字的某次方（这里是计算3的10次方）。它用起始值1乘以3，循环10次。这种计算并不需要知道当前是第几次循环（循环的计数器），只需要保证它执行次数是正确的即可。

我们还可以使用```for-in```遍历数组中的元素:

```
“let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    println("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
// Hello, Jack!”

```
你也同样可以遍历字典中的key-value。遍历时，字典中的每个元素都以```(key,value)```元组结构返回，你也可以在```for-in```中将元组中的key,value当做常量显式的分解出来。这里，key被分解为为常量```animalName```,value被分解为```legCount```：

```
“let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    println("\(animalName)s have \(legCount) legs")
}
// spiders have 8 legs
// ants have 6 legs
// cats have 4 legs”

```
```Dictionary```中的元素的顺序在被遍历时可能和我们插入它的顺序不同，这是由于```Dictionary```自身就是无序的，它在被遍历时无法保证元素的顺序。想了解更多关于数组和字典的内容，请查阅Collection Type一章。

除了数组和字典，你同样可以使用```for-in```来遍历字符串中的```Character```：

```
“for character in "Hello" {
    println(character)
}
// H
// e
// l
// l
// o

```
## For-Condition-Increment

除了使用```for-in```这种循环表达式，Swift还提供了传统的C风格的``for```循环表达式，通常它需要一个循环执行条件和一个累加器：

```
“for var index = 0; index < 3; ++index {
    println("index is \(index)")
}
// index is 0
// index is 1
// index is 2
```
下面是这种语法通用的表达式：

for ```initialization```;```condition```;```increment```{
```statements```	
}

和C语言一样，循环表达式被分号分割为3部分。但是和C语言不同的是，Swift不需要使用括号将"initialization;condition;increment"包围起来。

循环执行顺序如下：

1，循环开始时执行一次initialization表达式，初始化循环使用的常量或变量。

2，condition表达式被执行，如果结果为```false```循环结束，执行循环体后面的代码。如果condition表达式结果为```true```，继续执行循环体内的代码

3，当循环体内的代码被执行完时，increment表达式被执行。通常情况是增加或减少计数器的值，然后执行第2步，condition表达式会被再次执行。

上面的for循环结构也可以如下表示：

```initialization```
while ```condition``` {
```statements```
```increment```
}

在for循环初始化时创建的变量或者常量只在循环体内有效，如果想获取循环结束时的```index```值，你必须将```index```显式的声明到循环表达式前：

```
var index: Int
for index = 0; index < 3; ++index {
    println("index is \(index)")
}
// index is 0
// index is 1
// index is 2
println("The loop statements were executed \(index) times")
// prints "The loop statements were executed 3 times”

```
注意循环结束时，```index```值是```3```而不是```2```。当```++index```被最后一次执行时，```index```被赋值为```3```，这回导致```index<3```返回```false```，结束循环。

##While循环

一个```while```语句会循环执行一段代码直到条件变为```false```。这种循环语句在处理循环次数不确定的情况时非常有效。Swift提供两种```while```循环：

* ```while```语句会在执行循环提前判断执行条件。
* ```do-while```语句会在执行完循环体内代码后判断执行条件。

###while

一个```while```循环从判断执行条件开始。如果条件为```true```，则循环执行循环体内的代码，知道条件变为```false```。下面是通用的```while```语法格式：

```
while condition {
    statements
}
```
下面是一个简单的Snakes and Ladders游戏（也叫Chutes and Ladders）

【图】

游戏规则如下：

* 板子上有25个方块，你的目标是到达或超过第25个方格。
* 每次你需要通过掷骰子来决定前进几个放格，前进的方向由上图虚线的箭头所示。
* 如果在你的回合结束时，你恰好到了梯子的尾部，你可以沿着梯子爬上去。
* 如果在你的回合结束时，你恰好到了蛇的头部，则你会沿着蛇身滑下去。

游戏的板子可以看做是一个```Int```型的数组。大小由常量```finalSquare```决定，这个常量也会用来初始化数组和判断获胜条件。数组被初始化为26个0，注意不是25（数组范围从0到25）：

```
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)”
```
板子上的许多方格用来被指定为梯子或者蛇。如果是梯子，那么这个方格的值为正数，如果是蛇，则方格的值为负数：

```
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08

```
第三个方格被认定为是梯子的底部，它会让你走到第11个方格。为了表达这个意思,```board[03]```被复制为```+08```，它等价于整数8，考虑到所有的数字均为2位数，为了对齐和美观，（```+i```）用来和(```-i```)保持一致。

玩家从板子左下角的第0号方块开始，第一次掷骰子会将玩家移动到：

```
var square = 0
var diceRoll = 0
while square < finalSquare {
    // roll the dice
    if ++diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
    if square < board.count {
        // if we're still on the board, move up or down for a snake or a ladder
        square += board[square]
    }
}
println("Game over!")
```
这个例子用了一个非常简单的方式来掷骰子。我们没有采用每次产生一个随机数的方法，取而代之的是我们先给```diceRoll```赋值为0,然后在每次while循环的过程中对```diceRoll```加1，然后检测它的值是否等于7，让它等于7的时候，再将它重置为1。这样，产生的一系列```diceRoll```的值为1，2，3，4，5，6，1，2...。

在掷完骰子后，玩家前进```diceRoll```个方格。玩家在前进的过程中很可能超过25，这种情况下游戏会结束。为了解决这种情况，当```square```在累加```board[quare]```的值前，会检查```square```的值是否小于```board.count```的值，同样它也会规避由数组越界带来的错误。

然后```while```循环体结束，这时会再次判断循环执行条件，如果玩家已经前进到了25或者越过了25，那么循环条件会返回```false```，游戏结束。

显然在上面这情况下，使用```while```循环是非常合适的，因为循环次数不确定，只能根据循环条件来判断是否要终止循环。

###Do-While
另一个```while```循环的变种是```do-while```表达式，它首先执行一次循环，然后在判断循环执行条件。如此反复，直到循环条件返回```false```。

下面是```do-while```表达式的格式：

```
do {
    statements
} while condition”

```

还是上面的蛇和梯子的例子，我们来使用```do-while```实现，初始化变量的过程同```while```循环：

```
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0

```
这次，我们首先来判断第一次遇到的是梯子还是蛇。因为没有梯子会把玩家直接送到25，所以这个判断是安全的。开始时，玩家的位置在"0"，```board[0]```的值永远为0：

```
do {
    // move up or down for a snake or ladder
    square += board[square]
    // roll the dice
    if ++diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
} while square < finalSquare
println("Game over!")
```

在判断遇到的时梯子还是蛇之后，我们掷骰子，玩家前进```diceRoll```个格子。当前循环结束。

这里的循环条件（```while square < finalSquare```）和前面相同，但它会在循环结束后被执行。```do-while```循环结构比前面的```while```更适合这个游戏。使用```do-while```时，```square+=board[square]```会立刻被执行，它省去了上个例子中对数组越界的判断。

##条件表达式
通常情况下我们需要在满足某种条件时执行一段代码或者在出错时执行另一段代码，也可能需要在某个值过大或过小时打印输出一些提示信息。这都需要你在代码中加入判断条件。

Swift提供了两种条件判断的表达式，它们是```if```和```switch```。

通常情况下，在条件分支比较少时，你使用```if```表达式，```switch```表达式用来处理复杂的判断条件和过多的条件分支，此外```switch```在模式匹配上非常有用。

###If

```If```表达式很简单，当判断条件为```true```时，执行一段代码：

```
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
}
// prints "It's very cold. Consider wearing a scarf.
```
上面的例子会判断温度是否小于等于32华氏度。如果是，打印一条消息。

```if```表达式通常和```else```搭配使用，当```if```表达式返回```false```时，```else```分支的代码会被执行：

```
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else {
    println("It's not that cold. Wear a t-shirt.")
}
// prints "It's not that cold. Wear a t-shirt.

```

这种情况下```if```和```else```两个分支中的一个一定会被执行到，你也可以将多个```if```表达式连起来使用：

```
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    println("It's really warm. Don't forget to wear sunscreen.")
} else {
    println("It's not that cold. Wear a t-shirt.")
}
// prints "It's really warm. Don't forget to wear sunscreen.
```
这里，多了一个```if```表达式用来判断特定的温度范围。最后的```else```语句是可选的：

```
temperatureInFahrenheit = 72
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    println("It's really warm. Don't forget to wear sunscreen.")
}
```

在这个例子中，温度不满足```if```和```else if ```的执行条件，因此没有信息会被打印出来。

###Switch

```switch```表达式会将一个值和多种模式进行匹配。匹配成功则执行该条件所对应的代码。```switch```是一种可以替换```if```进行条件判断的表达式。```switch```的语法格式如下：

```
switch some value to consider {
case value 1:
    respond to value 1
case value 2,
value 3:
    respond to value 2 or 3
default:
    otherwise, do something else
}
```
每个```switch```表达式都对应多个```case```表达式。除了可以用```case```表达式来比较具体的值以外，Swift提供了许多复杂的模式匹配，下一小节会详细介绍。

```switch```语句内包含多个代码执行分支，这点和```if```表达式很像。```switch```表达式决定了那个分支会被执行，通常是根据变量值来决定的。

每个```switch```表达式必须是完整的，意思是它提供的分支条件必须能涵盖所有情况，你可以定义一个默认的分支条件用来处理一些意外的条件。这种分支通常用关键字```default```表示，并且它必须是最后一个分支条件。

这个例子使用```switch```表达式类匹配一个小写字母变量```someCharacter```：

```
let someCharacter: Character = "e"
switch someCharacter {
case "a", "e", "i", "o", "u":
    println("\(someCharacter) is a vowel")
case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
"n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
    println("\(someCharacter) is a consonant")
default:
    println("\(someCharacter) is not a vowel or a consonant")
}
// prints "e is a vowel”
```
```switch```表达式的第一个```case```分支是匹配五个元音字母。同理，第二个```case```分支用来匹配所有的字符常量。

通常来说列举出所有的字符不太现实，因此```switch```表达式提供了```default```分支用来匹配所有其它的字符，这确保了```switch```表达式的完整性。


###没有隐式贯穿


和C语言或Objective-C相比，Swift中的```switch```表达式在执行完一条```case```分支的代码后，则认为```switch```语句执行完毕。在某个```case```分支没有```break```的情况下，不会继续执行下一条```case```分支的代码。这比C语言更简单和安全。

	注意：
	你也可以在```case```分支代码执行前使用```break```语句来跳出这个分支，详见后面的章节。
每条```case```分支的函数体必须至少包含一行可执行代码。下面的代码是不合法的：

```
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a":
case "A":
    println("The letter A")
default:
    println("Not the letter A")
}
// this will report a compile-time error
```

和C语言不同，```switch```表达式不会既匹配`"a"`又匹配`"A"`。遇到这种情况，编译器会给出错误提示。这条规则会避免意外的执行了其它分支的代码。

一条```case```分支也可以匹配多个判断条件，用逗号隔开:

```
switch some value to consider {
case value 1,
value 2:
    statements
}
```
	注意
	对于```switch```表达式的某个case分支，你可以通过使用```fallthrough```关键字来强制贯穿改```case```分支。
	更对细节在Fallthrough一节有所介绍
	
###区间匹配

```switch```表达式的```case```分支可以是一个值区间同样支持范围匹配。下面这个例子展示了如何使用区间匹配来输出任意数字对应的自然语言格式：

```
let count = 3_000_000_000_000
let countedThings = "stars in the Milky Way"
var naturalCount: String
switch count {
case 0:
    naturalCount = "no"
case 1...3:
    naturalCount = "a few"
case 4...9:
    naturalCount = "several"
case 10...99:
    naturalCount = "tens of"
case 100...999:
    naturalCount = "hundreds of"
case 1000...999_999:
    naturalCount = "thousands of"
default:
    naturalCount = "millions and millions of"
}
println("There are \(naturalCount) \(countedThings).")
// prints "There are millions and millions of stars in the Milky Way.
```

###元组

你可以使用元组在同一个```switch```表达式中测试多个值。元组中的每个元素可以是一个区间，也可以是不同的值。我们使用(_)来匹配任何可能的值。

下面的例子使用一个元组类型（```Int```,```Int```）的点(x,y)并用图标来描述它的分布：

```
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    println("(0, 0) is at the origin")
case (_, 0):
    println("(\(somePoint.0), 0) is on the x-axis")
case (0, _):
    println("(0, \(somePoint.1)) is on the y-axis")
case (-2...2, -2...2):
    println("(\(somePoint.0), \(somePoint.1)) is inside the box")
default:
    println("(\(somePoint.0), \(somePoint.1)) is outside of the box")
}
// prints "(1, 1) is inside the box

```

【图】

```switch```表达式用来判断这个点是否在原点；红色的X轴上；橘黄色的Y轴上；在蓝色的4x4的盒子内，还是在盒子外面。

不像C语言，Swift支持不同的```case```分支匹配同一个结果，在这个例子中，点(0,0)满足所有4个分之条件。这种情况下只有第一条```case```语句被执行。点(0,0)会首先匹配第一条```case(0,0)```，后面的```case```语句会被忽略掉。

###值绑定(Value Bindings)

```switch```表达式允许在一个```case```分支中，将待匹配的值绑定到一些常量或临时变量上。这就是值绑定。
下面的例子将使用值绑定的方法重写上面的代码：

```
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    println("on the x-axis with an x value of \(x)")
case (0, let y):
    println("on the y-axis with a y value of \(y)")
case let (x, y):
    println("somewhere else at (\(x), \(y))")
}
// prints "on the x-axis with an x value of 2

```
【图】

上面我们通过```switch```表达式判断了```anotherPoint```这个点是否在红色的X，y轴上或者在非轴上的任意位置。

上面三条```case```语句使用临时变量```x```,```y```来匹配```anotherPoint```中的值。第一条```case(let x, 0)```语句用来匹配所有```y```值为0的点，并把该点的```x```值赋值给常量```x```。同理，```case(0,let y)```匹配所有```x```值为0的点，并把该点得```y```值赋给常量```y```。

临时变量被声明后，它就可以用在```case```分支的代码中。本例中```x```,```y```在```println```方法中被打印出来。

注意到上面的```switch```语句并没有```default```分支，原因是最后一条```case let(x,y)```涵盖了所有其他情况，因此我们不需要再写一个```default```分支了。

在上面的例子中，我们通过```let```关键字将```x```,```y```声明为常量，原因是我们不需要修改他们的值。同样我们也可以用```var```关键字声明他们为变量，如果把它们声明为变量则需要为他们指定合适的初始值。任何对于它们值的修改也仅仅局限在```case```分支的代码中有效。

###Where

在```case```语句的条件分支中可以使用```where```关键字增加附加条件的判断。

还是上面的例子：

```
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    println("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    println("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    println("(\(x), \(y)) is just some arbitrary point")
}
// prints "(1, -1) is on the line x == -y
```
【图】

上面的```switch```表达式用来检测```yetAnotherPoint```这个点是否在绿色或紫色的对角线上。

上面的三条```switch```表达式声明了常量```x```和```y```用来临时保存```yetAnotherPoint```中的坐标值。这两个常量同时也被```where```用来创建一个过滤条件。只有当```where```的过滤条件返回```true```时，```case```分支的代码才会被执行。

和上面的例子一样```default```分支在这个例子中也可以被忽略。

###控转移表达式

控制转移表达式会改变代码执行的顺序。Swift提供了4个控制转移表达式：

* continue
* break
* fallthrough
* return

我们下面将会讨论```control```,```break````,```return```表达式，```return```将会在函数一章讨论。



###continue

```continue```用来终止当前循环并开始执行下一次循环。它会说“本次循环结束了”，但并不会跳出循环。

	注意：
	在```for-condition-increment```一节，即使执行了```continue```，循环的累加器仍会自动加1。
	循环会继续，仅仅是循环体内的代码不会被执行。
下面的例子会移除一个小写字符串中所有的原因字母：

```
let puzzleInput = "great minds think alike"
var puzzleOutput = ""
for character in puzzleInput {
    switch character {
    case "a", "e", "i", "o", "u", " ":
        continue
    default:
        puzzleOutput += character
    }
}
println(puzzleOutput)
// prints "grtmndsthnklk
```

在上面的代码中，一旦出现元音字母，当前循环就会被终止，并重新开始下一次循环。这会让```switch```表达式去匹配元音字符或空字符时不做处理，而不是让每一个匹配到的字符都被打印出来。

###break

```break```语句会立刻终止当前执行的整个控制流。```break```可被用在```switch```表达式里面或循环中用来提前结束控制流。

###循环体内的break

当在循环体内执行```break```时，会退出整个循环，代码从循环体后面的第一行开始执行。

###Switch表达式中得break

当在```switch```中使用```break```时，会立即终止改```switch``代码块的执行，并且跳转到```switch```代码块结束的大括号(```}```)后的第一行代码。

这种行为可被用来忽略或跳过```switch```中的某个```case```。由于Swift要求```switch```的分支条件必须完整并且不允许空的```case```分支，因此在有些情况下使用```break```特意跳出某个分支会很必要。你可以通过在```case```的代码快中加入```break````来达到这个效果。当```case```分支的代码块被执行时，```break```会终止```switch```语句的执行。

	注意：
	当```switch```的一个分支仅仅包含注释时，编译器会给出错误提示。
	注释并不是真正的代码，他不能达到忽略这个```case```分支的作用。有哪次还是需要使用```break```。
	
下面这个例子用来判断一个字符的值是否是数字符号。为了简便，多个值被包含到一个分支中：

```
let numberSymbol: Character = "三"  // Simplified Chinese for the number 3
var possibleIntegerValue: Int?
switch numberSymbol {
case "1", "١", "一", "๑":
    possibleIntegerValue = 1
case "2", "٢", "二", "๒":
    possibleIntegerValue = 2
case "3", "٣", "三", "๓":
    possibleIntegerValue = 3
case "4", "٤", "四", "๔":
    possibleIntegerValue = 4
default:
    break
}
if let integerValue = possibleIntegerValue {
    println("The integer value of \(numberSymbol) is \(integerValue).")
} else {
    println("An integer value could not be found for \(numberSymbol).")
}
// prints "The integer value of 三 is 3."

```
这个例子用来判断```numberSymbol```是否是拉丁文，阿拉伯文，中文或泰语中的1到4之一。如果被匹配到，该```switch```分支语句给```Int?```类型变量```possibleIntegerValue```设置一个整数值。

当switch代码块执行完后，接下来的代码先判断```possibleIntegerValue``是否被绑定成功。因为是可选类型的缘故，```possibleIntegerValue```有一个隐式的初始值nil，所以仅仅当```possibleIntegerValue```曾被switch代码块的前四个分支中的某个设置过一个值时，可选的绑定将会被判定为成功。

在上面的例子中，想要把```Character```所有的的可能性都枚举出来是不现实的，所以使用```default```分支来包含所有上面没有匹配到字符的情况。由于这个```default```分支不需要执行任何动作，所以它只写了一条```break```语句。一旦落入到```default```分支中后，```break```语句就完成了该分支的所有代码操作，代码继续向下，开始执行```if let```语句。


