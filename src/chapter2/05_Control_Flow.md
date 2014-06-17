# 控制流(Control Flow)

## by moxin.xt

Swift提供类似C语言的控制流语法，比如```for```和```while```循环;```if```和```switch```的条件判断表达式以及``` break```,```continue```这种跳出循环的语句。

Swift除了支持类似C语言这种```for-condition-increment```的表达式外，还支持```for-in```这种循环语句，可以轻松的遍历数组，字典，字符串等序列。

Swift的```switch```语句和C语言相比很强大，它不会像C语言那样，因为在case的分支中忘记写break而执行了下一条case的语句。同时case语句可以匹配任何类型


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
这个例子用了一个非常简单的方式来掷骰子。
