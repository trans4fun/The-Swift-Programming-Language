# 控制流(Control Flow)

Swift provides all the familiar control flow constructs of C-like languages. These include for and while loops to perform a task multiple times; if and switch statements to execute different branches of code based on certain conditions; and statements such as break and continue to transfer the flow of execution to another point in your code.

Swift提供类似C语言的控制流语法，比如```for```和```while```循环;```if```和```switch```的条件判断语句语句以及``` break```,```continue```这种跳出循环的语句。

In addition to the traditional for-condition-increment loop found in C, Swift adds a for-in loop that makes it easy to iterate over arrays, dictionaries, ranges, strings, and other sequences.

Swift除了支持类似C语言这种```for-condition-increment```的语句外，还支持```for-in```这种循环语句，可以轻松的遍历数组，字典，字符串等序列。

Swift’s switch statement is also considerably more powerful than its counterpart in C. The cases of a switch statement do not “fall through” to the next case in Swift, avoiding common C errors caused by missing break statements. Cases can match many different types of pattern, including range matches, tuples, and casts to a specific type. Matched values in a switch case can be bound to temporary constants or variables for use within the case’s body, and complex matching conditions can be expressed with a where clause for each case.

Swift的```switch```语句和C语言相比很强大，它不会像C语言那样，因为在case的分支中忘记写break而执行了下一条case的语句。同时case语句可以进行不同类型的模式匹配，包括区间匹配，元组匹配和特定类型描述。```switch```语句中待匹配的值可以绑定到临时变量或常量上，便于```case```中得代码访问，同时，一些复杂的匹配条件可已通过```where```关键字来补充。


#For循环

A for loop performs a set of statements a certain number of times. Swift provides two kinds of for loop:

for循环可以将一段代码执行若干次。Swift提供两种for循环：

for-in performs a set of statements for each item in a range, sequence, collection, or progression.
for-condition-increment performs a set of statements until a specific condition is met, typically by incrementing a counter each time the loop ends.

* ```for-in```遍历并返回序列或集合中的每一个元素，执行一段代码
* ```for-condition-increment```在符合某种条件下（通常是在每次循环结束时对计数器+1），返回序列或集合中的每一个元素，执行一段代码。

##For-In

You use the for-in loop to iterate over collections of items, such as ranges of numbers, items in an array, or characters in a string.

你可以使用```for-in```来遍历集合里的元素;一定范围内的数字;数组中的元素或者字符串中的字符。

This example prints the first few entries in the five-times-table:

下面这个例子可以打印出一个5次循环的结果：

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

The collection of items being iterated is a closed range of numbers from 1 to 5 inclusive, as indicated by the use of the closed range operator (...). The value of index is set to the first number in the range (1), and the statements inside the loop are executed. In this case, the loop contains only one statement, which prints an entry from the five-times-table for the current value of index. After the statement is executed, the value of index is updated to contain the second value in the range (2), and the println function is called again. This process continues until the end of the range is reached.

我们首先通过(```...```)语句创建了一个数字集合，然后枚举集合中的每个元素，```index```值首先被赋值为range(```1```),然后执行循环体内的代码,上面这个例子中循环体内只有一行代码，作用是打印出```index```的值。当这行代码执行完后，```index```值会被更新，被赋值为range(```2```),```println```再次被调用，如此反复，直到循环结束。

In the example above, index is a constant whose value is automatically set at the start of each iteration of the loop. As such, it does not have to be declared before it is used. It is implicitly declared simply by its inclusion in the loop declaration, without the need for a let declaration keyword.

上面例子中```index```是个常量，在每次循环开始的时候会被自动赋值，因此它不需要在使用前通过```let```声明，因为它会被```for-in```隐式声明。

>注意
	
>常量```index```的作用域只存在于循环体内。如果你想在循环体外查看```index```的值或者使用它,你需要在循环开始前声明它。

If you don’t need each value from the range, you can ignore the values by using an underscore in place of a variable name:

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

This example calculates the value of one number to the power of another (in this case, 3 to the power of 10). It multiplies a starting value of 1 (that is, 3 to the power of 0) by 3, ten times, using a half-closed loop that starts with 0 and ends with 9. This calculation doesn’t need to know the individual counter values each time through the loop—it simply needs to execute the loop the correct number of times. The underscore character _ (used in place of a loop variable) causes the individual values to be ignored and does not provide access to the current value during each iteration of the loop.

这个例子用来计算某个数字的某次方（这里是计算3的10次方）。它用起始值1乘以3，循环10次。这种计算并不需要知道当前是第几次循环（循环的计数器），只需要保证它执行次数是正确的即可。

Use the for-in loop with an array to iterate over its items:我们还可以

使用```for-in```遍历数组中的元素:

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

You can also iterate over a dictionary to access its key-value pairs. Each item in the dictionary is returned as a (key, value) tuple when the dictionary is iterated, and you can decompose the (key, value) tuple’s members as explicitly named constants for use within in the body of the for-in loop. Here, the dictionary’s keys are decomposed into a constant called animalName, and the dictionary’s values are decomposed into a constant called legCount:

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

Items in a Dictionary may not necessarily be iterated in the same order as they were inserted. The contents of a Dictionary are inherently unordered, and iterating over them does not guarantee the order in which they will be retrieved. For more on arrays and dictionaries, see Collection Types.

Dictionary中的元素的顺序在被遍历时可能和我们插入它的顺序不同，这是由于```Dictionary```自身就是无序的，它在被遍历时无法保证元素的顺序。想了解更多关于数组和字典的内容，请查阅[集合类型](link)一章。

In addition to arrays and dictionaries, you can also use the for-in loop to iterate over the Character values in a string:

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

In addition to for-in loops, Swift supports traditional C-style for loops with a condition and an incrementer:

除了使用```for-in```这种循环语句，Swift还提供了传统的C风格的``for```循环语句，通常它需要一个循环执行条件和一个累加器：

```
“for var index = 0; index < 3; ++index {
    println("index is \(index)")
}
// index is 0
// index is 1
// index is 2
```

Here’s the general form of this loop format:

下面是这种语法通用的语句：

for ```initialization```;```condition```;```increment```{
```statements```	
}

Semicolons separate the three parts of the loop’s definition, as in C. However, unlike C, Swift doesn’t need parentheses around the entire “initialization; condition; increment” block.

和C语言一样，循环语句被分号分割为3部分。但是和C语言不同的是，Swift不需要使用括号将"initialization;condition;increment"包围起来。

The loop is executed as follows:

1,When the loop is first entered, the initialization expression is evaluated once, to set up any constants or variables that are needed for the loop.
2,The condition expression is evaluated. If it evaluates to false, the loop ends, and code execution continues after the for loop’s closing brace (}). If the expression evaluates to true, code execution continues by executing the statements inside the braces.
3,After all statements are executed, the increment expression is evaluated. It might increase or decrease the value of a counter, or set one of the initialized variables to a new value based on the outcome of the statements. After the increment expression has been evaluated, execution returns to step 2, and the condition expression is evaluated again.

循环执行顺序如下：

1，循环开始时执行一次initialization语句，初始化循环使用的常量或变量。

2，condition语句被执行，如果结果为```false```循环结束，执行循环体后面的代码。如果condition语句结果为```true```，继续执行循环体内的代码

3，当循环体内的代码被执行完时，increment语句被执行。通常情况是增加或减少计数器的值，然后执行第2步，condition语句会被再次执行。

The loop format and execution process described above is shorthand for (and equivalent to) the outline below:

上面的for循环结构也可以如下表示：

```initialization```
while ```condition``` {
```statements```
```increment```
}

Constants and variables declared within the initialization expression (such as var index = 0) are only valid within the scope of the for loop itself. To retrieve the final value of index after the loop ends, you must declare index before the loop’s scope begins:

在for循环初始化时创建的变量或者常量只在循环体内有效，如果想获取循环结束时的```index```值，你必须将```index```显式的声明到循环语句前：

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
Note that the final value of index after this loop is completed is 3, not 2. The last time the increment statement ++index is called, it sets index to 3, which causes index < 3 to equate to false, ending the loop.

注意循环结束时，```index```值是```3```而不是```2```。当```++index```被最后一次执行时，```index```被赋值为```3```，这回导致```index<3```返回```false```，结束循环。

##While循环

A while loop performs a set of statements until a condition becomes false. These kinds of loops are best used when the number of iterations is not known before the first iteration “begins. Swift provides two kinds of while loop:

while evaluates its condition at the start of each pass through the loop.
do-while evaluates its condition at the end of each pass through the loop.

一个```while```语句会循环执行一段代码直到条件变为```false```。这种循环语句在处理循环次数不确定的情况时非常有效。Swift提供两种```while```循环：

* ```while```语句会在执行循环提前判断执行条件。
* ```do-while```语句会在执行完循环体内代码后判断执行条件。

###while

A while loop starts by evaluating a single condition. If the condition is true, a set of statements is repeated until the condition becomes false.

Here’s the general form of a while loop:

一个```while```循环从判断执行条件开始。如果条件为```true```，则循环执行循环体内的代码，知道条件变为```false```。下面是通用的```while```语法格式：

```
while condition {
    statements
}
```

This example plays a simple game of Snakes and Ladders (also known as Chutes and Ladders):

下面是一个简单的Snakes and Ladders游戏（也叫Chutes and Ladders）

【图】

The rules of the game are as follows:

The board has 25 squares, and the aim is to land on or beyond square 25.
Each turn, you roll a six-sided dice and move by that number of squares, following the horizontal path indicated by the dotted arrow above.
If your turn ends at the bottom of a ladder, you move up that ladder.
If your turn ends at the head of a snake, you move down that snake.

游戏规则如下：

* 板子上有25个方块，你的目标是到达或超过第25个方格。
* 每次你需要通过掷骰子来决定前进几个放格，前进的方向由上图虚线的箭头所示。
* 如果在你的回合结束时，你恰好到了梯子的尾部，你可以沿着梯子爬上去。
* 如果在你的回合结束时，你恰好到了蛇的头部，则你会沿着蛇身滑下去。

The game board is represented by an array of Int values. Its size is based on a constant called finalSquare, which is used to initialize the array and also to check for a win condition later in the example. The board is initialized with 26 zero Int values, not 25 (one each at indices 0 through 25 inclusive):

游戏的板子可以看做是一个```Int```型的数组。大小由常量```finalSquare```决定，这个常量也会用来初始化数组和判断获胜条件。数组被初始化为26个0，注意不是25（数组范围从0到25）：

```
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)”
```

Some squares are then set to have more specific values for the snakes and ladders. Squares with a ladder base have a positive number to move you up the board, whereas squares with a snake head have a negative number to move you back down the board:

板子上的许多方格用来被指定为梯子或者蛇。如果是梯子，那么这个方格的值为正数，如果是蛇，则方格的值为负数：

```
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08

```
Square 3 contains the bottom of a ladder that moves you up to square 11. To represent this, board[03] is equal to +08, which is equivalent to an integer value of 8 (the difference between 3 and 11). The unary plus operator (+i) balances with the unary minus operator (-i), and numbers lower than 10 are padded with zeros so that all board definitions align. (Neither stylistic tweak is strictly necessary, but they lead to neater code.)

第三个方格被认定为是梯子的底部，它会让你走到第11个方格。为了表达这个意思,```board[03]```被复制为```+08```，它等价于整数8，考虑到所有的数字均为2位数，为了对齐和美观，（```+i```）用来和(```-i```)保持一致。

The player’s starting square is “square zero”, which is just off the bottom left corner of the board. The first dice roll always moves the player on to the board:

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

This example uses a very simple approach to dice rolling. Instead of a random number generator, it starts with a diceRoll value of 0. Each time through the while loop, diceRoll is incremented with the prefix increment operator (++i), and is then checked to see if it has become too large. The return value of ++diceRoll is equal to the value of diceRoll after it is incremented. Whenever this return value equals 7, the dice roll has become too large, and is reset to a value of 1. This gives a sequence of diceRoll values that is always 1, 2, 3, 4, 5, 6, 1, 2 and so on.

这个例子用了一个非常简单的方式来掷骰子。我们没有采用每次产生一个随机数的方法，取而代之的是我们先给```diceRoll```赋值为0,然后在每次while循环的过程中对```diceRoll```加1，然后检测它的值是否等于7，让它等于7的时候，再将它重置为1。这样，产生的一系列```diceRoll```的值为1，2，3，4，5，6，1，2...。

After rolling the dice, the player moves forward by diceRoll squares. It’s possible that the dice roll may have moved the player beyond square 25, in which case the game is over. To cope with this scenario, the code checks that square is less than the board array’s count property before adding the value stored in board[square] onto the current square value to move the player up or down any ladders or snakes.

在掷完骰子后，玩家前进```diceRoll```个方格。玩家在前进的过程中很可能超过25，这种情况下游戏会结束。为了解决这种情况，当```square```在累加```board[quare]```的值前，会检查```square```的值是否小于```board.count```的值，同样它也会规避由数组越界带来的错误。

Had this check not been performed, board[square] might try to access a value outside the bounds of the board array, which would trigger an error. If square is now equal to 26, the code would try to check the value of board[26], which is larger than the size of the array.

由于做了这种校验，当board[square]发生数组越界的情况时，会引发错误。例如，如果当前方格的值为26，代码会试图访问board[26],显然这个访问会引发数组越界。

The current while loop execution then ends, and the loop’s condition is checked to see if the loop should be executed again. If the player has moved on or beyond square number 25, the loop’s condition evaluates to false, and the game ends.

然后```while```循环体结束，这时会再次判断循环执行条件，如果玩家已经前进到了25或者越过了25，那么循环条件会返回```false```，游戏结束。

A while loop is appropriate in this case because the length of the game is not clear at the start of the while loop. Instead, the loop is executed until a particular condition is satisfied

显然在上面这情况下，使用```while```循环是非常合适的，因为循环次数不确定，只能根据循环条件来判断是否要终止循环。

###Do-While

The other variation of the while loop, known as the do-while loop, performs a single pass through the loop block first, before considering the loop’s condition. It then continues to repeat the loop until the condition is false.

Here’s the general form of a do-while loop:
另一个```while```循环的变种是```do-while```语句，它首先执行一次循环，然后在判断循环执行条件。如此反复，直到循环条件返回```false```。

下面是```do-while```语句的格式：

```
do {
    statements
} while condition”

```
Here’s the Snakes and Ladders example again, written as a do-while loop rather than a while loop. The values of finalSquare, board, square, and diceRoll are initialized in exactly the same way as with a while loop:

还是上面的蛇和梯子的例子，我们来使用```do-while```实现，初始化变量的过程同```while```循环：

```
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0

```

In this version of the game, the first action in the loop is to check for a ladder or a snake. No ladder on the board takes the player straight to square 25, and so it is not possible to win the game by moving up a ladder. Therefore, it is safe to check for a snake or a ladder as the first action in the loop.

At the start of the game, the player is on “square zero”. board[0] always equals 0, and has no effect:

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
After the code checks for snakes and ladders, the dice is rolled, and the player is moved forward by diceRoll squares. The current loop execution then ends.

在判断遇到的时梯子还是蛇之后，我们掷骰子，玩家前进```diceRoll```个格子。当前循环结束。

The loop’s condition (while square < finalSquare) is the same as before, but this time it is not evaluated until the end of the first run through the loop. The structure of the do-while loop is better suited to this game than the while loop in the previous example. In the do-while loop above, square += board[square] is always executed immediately after the loop’s while condition confirms that square is still on the board. This behavior removes the need for the array bounds check seen in the earlier version of the game.

这里的循环条件（```while square < finalSquare```）和前面相同，但它会在循环结束后被执行。```do-while```循环结构比前面的```while```更适合这个游戏。使用```do-while```时，```square+=board[square]```会立刻被执行，它省去了上个例子中对数组越界的判断。

##条件语句

It is often useful to execute different pieces of code based on certain conditions. You might want to run an extra piece of code when an error occurs, or to display a message when a value becomes too high or too low. To do this, you make parts of your code conditional.

通常情况下我们需要在满足某种条件时执行一段代码或者在出错时执行另一段代码，也可能需要在某个值过大或过小时打印输出一些提示信息。这都需要你在代码中加入判断条件。

Swift provides two ways to add conditional branches to your code, known as the if statement and the switch statement. Typically, you use the if statement to evaluate simple conditions with only a few possible outcomes. The switch statement is better suited to more complex conditions with multiple possible permutations, and is useful in situations where pattern-matching can help select an appropriate code branch to execute.

Swift提供了两种条件判断的语句，它们是```if```和```switch```。通常情况下，在条件分支比较少时，你使用```if```语句，```switch```语句用来处理复杂的判断条件和过多的条件分支，此外```switch```在模式匹配上非常有用。

###If

In its simplest form, the if statement has a single if condition. It executes a set of statements only if that condition is true:

```If```语句很简单，当判断条件为```true```时，执行一段代码：

```
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
}
// prints "It's very cold. Consider wearing a scarf.
```

The preceding example checks whether the temperature is less than or equal to 32 degrees Fahrenheit (the freezing point of water). If it is, a message is printed. Otherwise, no message is printed, and code execution continues after the if statement’s closing brace.

上面的例子会判断温度是否小于等于32华氏度。如果是，打印一条消息,否则，则没有信息输出，执行if代码段后面的代码。

The if statement can provide an alternative set of statements, known as an else clause, for when the if condition is false. These statements are indicated by the else keyword:

```if```语句通常和```else```搭配使用，当```if```语句返回```false```时，```else```分支的代码会被执行：

```
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else {
    println("It's not that cold. Wear a t-shirt.")
}
// prints "It's not that cold. Wear a t-shirt.

```
One of these two branches is always executed. Because the temperature has increased to 40 degrees Fahrenheit, it is no longer cold enough to advise wearing a scarf, and so the else branch is triggered instead.

这种情况下```if```和```else```两个分支中的一个一定会被执行到。因为温度已经升高到40华氏度，不需要再建议带围巾了，因此else语句的代码段被执行。

You can chain multiple if statements together, to consider additional clauses:

你也可以将多个```if```语句连起来使用：

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

Here, an additional if statement is added to respond to particularly warm temperatures. The final else clause remains, and prints a response for any temperatures that are neither too warm nor too cold.

这里，多了一个```if```语句用来判断特定的温度范围。仍然有一个```else```在最后面，当温度既不高又不低得情况下打印出相应的信息：

最后的```else```语句是可选的，如果它所在的分支不不需要执行，则可以将它排除：

```
temperatureInFahrenheit = 72
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    println("It's really warm. Don't forget to wear sunscreen.")
}
```
In this example, the temperature is neither too cold nor too warm to trigger the if or else if conditions, and so no message is printed.

在这个例子中，温度不满足```if```和```else if ```的执行条件，因此没有信息会被打印出来。

###Switch

A switch statement considers a value and compares it against several possible matching patterns. It then executes an appropriate block of code, based on the first pattern that matches successfully. A switch statement provides an alternative to the if statement for responding to multiple potential states.

一条```switch```语句会将一个值和多种模式进行匹配。匹配成功则执行该条件所对应的代码。```switch```是一种可以替换```if```进行条件判断的语句。

In its simplest form, a switch statement compares a value against one or more values of the same type：

最简单的```switch```的语法是用来比较一个或多个类型相同的值：

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

Every switch statement consists of multiple possible cases, each of which begins with the case keyword. In addition to comparing against specific values, Swift provides several ways for each case to specify more complex matching patterns. These options are described later in this section.

每个```switch```语句都对应多个```case```语句。除了可以用```case```语句来比较具体的值以外，Swift提供了许多复杂的模式匹配，下一小节会详细介绍。

The body of each switch case is a separate branch of code execution, in a similar manner to the branches of an if statement. The switch statement determines which branch should be selected. This is known as switching on the value that is being considered.

```switch```语句内包含多个代码执行分支，这点和```if```语句很像。```switch```语句决定了那个分支会被执行，通常是根据变量值来决定的。

Every switch statement must be exhaustive. That is, every possible value of the type being considered must be matched by one of the switch cases. If it is not appropriate to provide a switch case for every possible value, you can define a default catch-all case to cover any values that are not addressed explicitly. This catch-all case is indicated by the keyword default, and must always appear last.


每个```switch```语句必须是完整的，意思是它提供的分支条件必须能涵盖所有情况，你可以定义一个默认的分支条件用来处理一些意外的条件。这种分支通常用关键字```default```表示，并且它必须是最后一个分支条件。

This example uses a switch statement to consider a single lowercase character called someCharacter:

这个例子使用```switch```语句类匹配一个小写字母变量```someCharacter```：

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
The switch statement’s first case matches all five lowercase vowels in the English language. Similarly, its second case matches all lowercase English consonants.

```switch```语句的第一个```case```分支是匹配五个元音字母。同理，第二个```case```分支用来匹配所有的字符常量。

It is not practical to write all other possible characters as part of a switch case, and so this switch statement provides a default case to match all other characters that are not vowels or consonants. This provision ensures that the switch statement is exhaustive.

通常来说列举出所有的字符不太现实，因此```switch```语句提供了```default```分支用来匹配所有其它的字符，这确保了```switch```语句的完整性。


###没有隐式贯穿

In contrast with switch statements in C and Objective-C, switch statements in Swift do not fall through the bottom of each case and into the next one by default. Instead, the entire switch statement finishes its execution as soon as the first matching switch case is completed, without requiring an explicit break statement. This makes the switch statement safer and easier to use than in C, and avoids executing more than one switch case by mistake.

和C语言或Objective-C相比，Swift中的```switch```语句在执行完一条```case```分支的代码后，则认为```switch```语句执行完毕。在某个```case```分支没有```break```的情况下，不会继续执行下一条```case```分支的代码。这比C语言更简单和安全。

>注意：
>你也可以在```case```分支代码执行前使用```break```语句来跳出这个分支，详见后面的[switch语句中break一节](link)。

The body of each case must contain at least one executable statement. It is not valid to write the following code, because the first case is empty:

每条```case```分支的函数体必须至少包含一行可执行代码。下面的代码是不合法的,因为第一条case分支的函数体为空：

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

Unlike a switch statement in C, this switch statement does not match both "a" and "A". Rather, it reports a compile-time error that case "a": does not contain any executable statements. This approach avoids accidental fallthrough from one case to another, and makes for safer code that is clearer in its intent.

和C语言不同，```switch```语句不会既匹配`"a"`又匹配`"A"`。遇到这种情况，编译器会给出错误提示。这条规则会避免意外的执行了其它分支的代码。

Multiple matches for a single switch case can be separated by commas, and can be written over multiple lines if the list is long:

一条```case```分支也可以匹配多个判断条件，用逗号隔开:

```
switch some value to consider {
case value 1,
value 2:
    statements
}
```
>注意
>对于```switch```语句的某个case分支，你可以通过使用```fallthrough```关键字来强制贯穿改```case```分支。
>更对细节在[Fallthrough](link)一节有所介绍
	
###区间匹配

Values in switch cases can be checked for their inclusion in a range. This example uses number ranges to provide a natural-language count for numbers of any size:

```switch```语句的```case```分支可以是一个值区间同样支持范围匹配。下面这个例子展示了如何使用区间匹配来输出任意数字对应的自然语言格式：

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

You can use tuples to test multiple values in the same switch statement. Each element of the tuple can be tested against a different value or range of values. Alternatively, use the underscore (_) identifier to match any possible value.

你可以使用元组在同一个```switch```语句中测试多个值。元组中的每个元素可以是一个区间，也可以是不同的值。我们使用(_)来匹配任何可能的值。

The example below takes an (x, y) point, expressed as a simple tuple of type (Int, Int), and categorizes it on the graph that follows the example:

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

The switch statement determines if the point is at the origin (0, 0); on the red x-axis; on the orange y-axis; inside the blue 4-by-4 box centered on the origin; or outside of the box.

```switch```语句用来判断这个点是否在原点；红色的X轴上；橘黄色的Y轴上；在蓝色的4x4的盒子内，还是在盒子外面。

Unlike C, Swift allows multiple switch cases to consider the same value or values. In fact, the point (0, 0) could match all four of the cases in this example. However, if multiple matches are possible, the first matching case is always used. The point (0, 0) would match case (0, 0) first, and so all other matching cases would be ignored.

不像C语言，Swift支持不同的```case```分支匹配同一个结果，在这个例子中，点(0,0)满足所有4个分之条件。这种情况下只有第一条```case```语句被执行。点(0,0)会首先匹配第一条```case(0,0)```，后面的```case```语句会被忽略掉。

###值绑定(Value Bindings)

A switch case can bind the value or values it matches to temporary constants or variables, for use in the body of the case. This is known as value binding, because the values are “bound” to temporary constants or variables within the case’s body.

```switch```语句允许在一个```case```分支中，将待匹配的值绑定到一些常量或临时变量上。这样就可以在case分支的代码段中使用这些变量或常量，这就是值绑定。

The example below takes an (x, y) point, expressed as a tuple of type (Int, Int) and categorizes it on the graph that follows:

下面的例子将定义一个(Int,Int)型的元组变量(x,y)，并归类它在图中的位置:

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

The switch statement determines if the point is on the red x-axis, on the orange y-axis, or elsewhere, on neither axis.

上面我们通过```switch```语句判断了```anotherPoint```这个点是否在红色的X，y轴上或者在非轴上的任意位置。

The three switch cases declare placeholder constants x and y, which temporarily take on one or both tuple values from anotherPoint. The first case, case (let x, 0), matches any point with a y value of 0 and assigns the point’s x value to the temporary constant x. Similarly, the second case, case (0, let y), matches any point with an x value of 0 and assigns the point’s y value to the temporary constant y.

上面三条```case```语句使用临时变量```x```,```y```来匹配```anotherPoint```中的值。第一条```case(let x, 0)```语句用来匹配所有```y```值为0的点，并把该点的```x```值赋值给常量```x```。同理，```case(0,let y)```匹配所有```x```值为0的点，并把该点得```y```值赋给常量```y```。

Once the temporary constants are declared, they can be used within the case’s code block. Here, they are used as shorthand for printing the values with the println function.

临时变量被声明后，它就可以用在```case```分支的代码中。本例中```x```,```y```在```println```方法中被打印出来。

Note that this switch statement does not have a default case. The final case, case let (x, y), declares a tuple of two placeholder constants that can match any value. As a result, it matches all possible remaining values, and a default case is not needed to make the switch statement exhaustive.

注意到上面的```switch```语句并没有```default```分支，原因是最后一条```case let(x,y)```涵盖了所有其他情况，因此我们不需要再写一个```default```分支了。

In the example above, x and y are declared as constants with the let keyword, because there is no need to modify their values within the body of the case. However, they could have been declared as variables instead, with the var keyword. If this had been done, a temporary variable would have been created and initialized with the appropriate value. Any changes to that variable would only have an effect within the body of the case.

在上面的例子中，我们通过```let```关键字将```x```,```y```声明为常量，原因是我们不需要修改他们的值。同样我们也可以用```var```关键字声明他们为变量，如果把它们声明为变量则需要为他们指定合适的初始值。任何对于它们值的修改也仅仅局限在```case```分支的代码中有效。

###Where

A switch case can use a where clause to check for additional conditions.

在```case```语句的条件分支中可以使用```where```关键字增加附加条件的判断。

The example below categorizes an (x, y) point on the following graph:

还是上面的例子,用来归类(x,y)点所在图中得位置：

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

The switch statement determines if the point is on the green diagonal line where x == y, on the purple diagonal line where x == -y, or neither.

上面的```switch```语句用来检测```yetAnotherPoint```这个点是否在绿色（x==y）或紫色(x==-y)的对角线上。

The three switch cases declare placeholder constants x and y, which temporarily take on the two tuple values from point. These constants are used as part of a where clause, to create a dynamic filter. The switch case matches the current value of point only if the where clause’s condition evaluates to true for that value.

上面的三条```switch```语句声明了常量```x```和```y```用来临时保存```yetAnotherPoint```中的坐标值。这两个常量同时也被```where```用来创建一个过滤条件。只有当```where```的过滤条件返回```true```时，```case```分支的代码才会被执行。

As in the previous example, the final case matches all possible remaining values, and so a default case is not needed to make the switch statement exhaustive.

和上面的例子一样```default```分支在这个例子中也可以被忽略。

###控转移语句

Control transfer statements change the order in which your code is executed, by transferring control from one piece of code to another. Swift has four control transfer statements:

控制转移语句会改变代码执行的顺序。Swift提供了4个控制转移语句：

* continue
* break
* fallthrough
* return

The control, break and fallthrough statements are described below. The return statement is described in Functions.

我们下面将会讨论```control```,```break````,```return```语句，```return```将会在[函数](link)一章讨论。



###continue

The continue statement tells a loop to stop what it is doing and start again at the beginning of the next iteration through the loop. It says “I am done with the current loop iteration” without leaving the loop altogether.

```continue```用来终止当前循环并开始执行下一次循环。它会说“本次循环结束了”，但并不会跳出循环。

>注意：
>在```for-condition-increment```一节，即使执行了```continue```，循环的累加器仍会自动加1。
>循环会继续，仅仅是循环体内的代码不会被执行。

The following example removes all vowels and spaces from a lowercase string to create a cryptic puzzle phrase:

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
The code above calls the continue keyword whenever it matches a vowel or a space, causing the current iteration of the loop to end immediately and to jump straight to the start of the next iteration. This behavior enables the switch block to match (and ignore) only the vowel and space characters, rather than requiring the block to match every character that should get printed.

在上面的代码中，一旦出现元音字母，当前循环就会被终止，并重新开始下一次循环。这会让```switch```语句去匹配元音字符或空字符时不做处理，而不是让每一个匹配到的字符都被打印出来。

###break

The break statement ends execution of an entire control flow statement immediately. The break statement can be used inside a switch statement or loop statement when you want to terminate the execution of the switch or loop statement earlier than would otherwise be the case.

```break```语句会立刻终止当前执行的整个控制流。```break```可被用在```switch```语句里面或循环中用来提前结束控制流。

###循环体内的break

When used inside a loop statement, break ends the loop’s execution immediately, and transfers control to the first line of code after the loop’s closing brace (}). No further code from the current iteration of the loop is executed, and no further iterations of the loop are started.

当在循环体内执行```break```时，会退出整个循环，代码从循环体后面的第一行开始执行,break语句后面的代码将不会执行，下一次循环也不会开始。

###Switch语句中得break

When used inside a switch statement, break causes the switch statement to end its execution immediately, and to transfer control to the first line of code after the switch statement’s closing brace (}).

当在```switch```中使用```break```时，会立即终止改```switch``代码块的执行，并且跳转到```switch```代码块结束的大括号(```}```)后的第一行代码。

This behavior can be used to match and ignore one or more cases in a switch statement. Because Swift’s switch statement is exhaustive and does not allow empty cases, it is sometimes necessary to deliberately match and ignore a case in order to make your intentions explicit. You do this by writing the break statement as the entire body of the case you want to ignore. When that case is matched by the switch statement, the break statement inside the case ends the switch

这种行为可被用来忽略或跳过```switch```中的某个```case```。由于Swift要求```switch```的分支条件必须完整并且不允许空的```case```分支，因此在有些情况下使用```break```特意跳出某个分支会很必要。你可以通过在```case```的代码快中加入```break````来达到这个效果。当```case```分支的代码块被执行时，```break```会终止```switch```语句的执行。

>注意：
>当```switch```的一个分支仅仅包含注释时，编译器会给出错误提示。
>注释并不是真正的代码，他不能达到忽略这个```case```分支的作用。有哪次还是需要使用```break```。

The following example switches on a Character value and determines whether it represents a number symbol in one of four languages. Multiple values are covered in a single switch case for brevity:
	
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

This example checks numberSymbol to determine whether it is a Latin, Arabic, Chinese, or Thai symbol for the numbers 1 to 4. If a match is found, one of the switch statement’s cases sets an optional Int? variable called possibleIntegerValue to an appropriate integer value.

这个例子用来判断```numberSymbol```是否是拉丁文，阿拉伯文，中文或泰语中的1到4之一。如果被匹配到，该```switch```分支语句给```Int?```类型变量```possibleIntegerValue```设置一个整数值。

After the switch statement completes its execution, the example uses optional binding to determine whether a value was found. The possibleIntegerValue variable has an implicit initial value of nil by virtue of being an optional type, and so the optional binding will succeed only if possibleIntegerValue was set to an actual value by one of the switch statement’s first four cases.

当switch代码块执行完后，接下来的代码先判断```possibleIntegerValue``是否被绑定成功。因为是可选类型的缘故，```possibleIntegerValue```有一个隐式的初始值nil，所以仅仅当```possibleIntegerValue```曾被switch代码块的前四个分支中的某个设置过一个值时，可选的绑定将会被判定为成功。

It is not practical to list every possible Character value in the example above, so a default case provides a catchall for any characters that are not matched. This default case does not need to perform any action, and so it is written with a single break statement as its body. As soon as the default statement is matched, the break statement ends the switch statement’s execution, and code execution continues from the if let statement.

在上面的例子中，想要把```Character```所有的的可能性都枚举出来是不现实的，所以使用```default```分支来包含所有上面没有匹配到字符的情况。由于这个```default```分支不需要执行任何动作，所以它只写了一条```break```语句。一旦落入到```default```分支中后，```break```语句就完成了该分支的所有代码操作，代码继续向下，开始执行```if let```语句。

###Fallthrough

Switch statements in Swift do not fall through the bottom of each case and into the next one. Instead, the entire switch statement completes its execution as soon as the first matching case is completed. By contrast, C requires you to insert an explicit break statement at the end of every switch case to prevent fallthrough. Avoiding default fallthrough means that Swift switch statements are much more concise and predictable than their counterparts in C, and thus they avoid executing multiple switch cases by mistake.

Swift中的Switch语句不会从上到下进入每一个case分支。相反，一旦有一个case分支被匹配成功，整个state语句就结束执行了。相比之下，在C语言中，为了防止switch语句会贯穿执行每一个case分支，你需要在每个case分支的末尾插入```break```语句。和C语言相比，Swift支持这种避免贯穿行为会让```switch```语句更简洁和更安全也能规避错误执行多个case分支的情况。

If you really need C-style fallthrough behavior, you can opt in to this behavior on a case-by-case basis with the fallthrough keyword. The example below uses fallthrough to create a textual description of a number:

如果你一定要使用C风格的贯穿(fallthrough)机制，你可以在每个需要支持该特性的case分支中使用```fallthrough```关键字。下面这个例子展示了如何使用```fallthrough```来实现对数字的文本描述：

```
let integerToDescribe = 5
var description = "The number \(integerToDescribe) is"
switch integerToDescribe {
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " a prime number, and also"
    fallthrough
default:
    description += " an integer."
}
println(description)
// prints "The number 5 is a prime number, and also an integer.
```

This example declares a new String variable called description and assigns it an initial value. The function then considers the value of integerToDescribe using a switch statement. If the value of integerToDescribe is one of the prime numbers in the list, the function appends text to the end of description, to note that the number is prime. It then uses the fallthrough keyword to “fall into” the default case as well. The default case adds some extra text to the end of the description, and the switch statement is complete.

这个例子中声明了一个叫```description```的```string```类型的变量，并且为其赋了初值。然后这个函数通过```switch```语句来判断```integerToDescribe```的值。如果```integerToDescribe```的值为数组中的一个素数，则该函数会为```decription```后面追加一段文本用来提示改数字式质数。然后会使用```fallthrough```关键字来执行```default```中的代码。在```default```分支中会为```description```后面继续追加一段文本。至此，```switch```语句才算执行完成。

If the value of integerToDescribe is not in the list of known prime numbers, it is not matched by the first switch case at all. There are no other specific cases, and so integerToDescribe is matched by the catchall default case.

如果```integerToDescribe```的值不在这组质数当中，则它不会和第一条```case```语句匹配。由于没有其它的分支存在，所以```integerToDescribe```会落入```default```分支。

After the switch statement has finished executing, the number’s description is printed using the println function. In this example, the number 5 is correctly identified as a prime number.

当```switch```语句执行完成后，关于这个数字的描述会通过```println```函数打印出来。在这个例子中，数字```5```被正确的识别为一个质数。

>注意：
>和C语言的```switch```语句一样，```fallthrough```不会检查它落入执行的```case```分支的条件是否匹配，
>它只是简单的执行下一条```case```(或```default```)中的代码。
	
###Labeled语句

You can nest loops and switch statements inside other loops and switch statements in Swift to create complex control flow structures. However, loops and switch statements can both use the break statement to end their execution prematurely. Therefore, it is sometimes useful to be explicit about which loop or switch statement you want a break statement to terminate. Similarly, if you have multiple nested loops, it can be useful to be explicit about which loop the continue statement should affect.

在```swift```中，可以在循环或```switch```函数中嵌套循环或```switch```函数来实现比较复杂的控制流结构。但是，在循环或```switch```函数中可以使用```break```语句提前终止其执行过程。因此，有些时候显示的调用```break```来标识终止循环或```switch```是非常有好处的。类似的，如果一个循环中嵌套了多个循环，使用```continue```来标识其影响的循环体也是很有用的。

To achieve these aims, you can mark a loop statement or switch statement with a statement label, and use this label with the break statement or continue statement to end or continue the execution of the labeled statement.

为了实现上面的目标，你可以通过标签来标识某个循环或```switch```语句。使用```break```或```continue```时，带上这个标签，这个标签可以用来结束或执行被标记的代码段。

A labeled statement is indicated by placing a label on the same line as the statement’s introducer keyword, followed by a colon. Here’s an example of this syntax for a while loop, although the principle is the same for all loops and switch statements


标签语句通常被放到一些关键字的前面，通过分号隔开。下面是一个通过标签来标记```while```语句的例子，循环或```switch```语句和它类似：

```
label name: while condition {
    statements
}

```

The following example uses the break and continue statements with a labeled while loop for an adapted version of the Snakes and Ladders game that you saw earlier in this chapter. This time around, the game has an extra rule:

下面这个例子将使用```break```和```continue```,配合带标签的```while```循环，该循环和前面的梯子和蛇的例子一直。这次，该游戏新增加了一条规则

* 为了胜利，你必须恰好到达第25个格子中

If a particular dice roll would take you beyond square 25, you must roll again until you roll the exact number needed to land on square 25.

如果某一次掷骰子会把你带到超过25的地方，必须重新掷骰子，直到你恰好到达第25号格子的位子

The game board is the same as before:”
游戏的棋盘和前面的一样：

【图】

The values of finalSquare, board, square, and diceRoll are initialized in the same way as before:

```finalSquare```,```board```,```square```和```diceRoll```的值和之前初始化的值相同:

```
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0

```
This version of the game uses a while loop and a switch statement to implement the game’s logic. The while loop has a statement label called gameLoop, to indicate that it is the main game loop for the Snakes and Ladders game.

这个版本会使用```while```循环和```switch```语句来实现游戏的逻辑。```while```循环有个标签叫做```gameLoop```，用来表示这个循环是这个游戏的主循环。

The while loop’s condition is while square != finalSquare, to reflect that you must land exactly on square 25:

```while```循环的条件是```while square != finalSquare```用来表示你必须正好落在第25个格子中：

```
gameLoop: while square != finalSquare {
    if ++diceRoll == 7 { diceRoll = 1 }
    switch square + diceRoll {
    case finalSquare:
        // diceRoll will move us to the final square, so the game is over
        break gameLoop
    case let newSquare where newSquare > finalSquare:
        // diceRoll will move us beyond the final square, so roll again
        continue gameLoop
    default:
        // this is a valid move, so find out its effect
        square += diceRoll
        square += board[square]
    }
}
println("Game over!")

```
The dice is rolled at the start of each loop. Rather than moving the player immediately, a switch statement is used to consider the result of the move, and to work out if the move is allowed:

在每个循环开始前都需要掷骰子，与之前立刻移动玩家不同，这次利用```switch```语句计算每次掷骰子产生的结果，从而决
定玩家是否可以移动：

If the dice roll will move the player onto the final square, the game is over. The break gameLoop statement transfers control to the first line of code outside of the while loop, which ends the game.

* 如果掷骰子的结果恰好将玩家移动到最后的方格中，那么游戏结束。```break gameLoop```会将代码跳到循环后的第一条语句，继续执行后面的代码。

If the dice roll will move the player beyond the final square, the move is invalid, and the player needs to roll again. The continue gameLoop statement ends the current while loop iteration and begins the next iteration of the loop.

* 如果掷骰子的结果将玩家移动到超过最后一个方格的位置，那么这次结果是无效的，玩家需要重新掷骰子。```continue gameLoop```会将当前循环终止并重新开始下一次循环。

In all other cases, the dice roll is a valid move. The player moves forward by diceRoll squares, and the game logic checks for any snakes and ladders. The loop then ends, and control returns to the while condition to decide whether another turn is required

* 在所有其余的情况中，掷骰子的结果是有效的，玩家会前进```diceRoll```个格子，游戏的逻辑会检测是否遇到梯子或者蛇。循环结束时，代码将回到```while```条件判定检查是否要进行下一次循环。

NOTE

If the break statement above did not use the gameLoop label, it would break out of the switch statement, not the while statement. Using the gameLoop label makes it clear which control statement should be terminated.

Note also that it is not strictly necessary to use the gameLoop label when calling continue gameLoop to jump to the next iteration of the loop. There is only one loop in the game, and so there is no ambiguity as to which loop the continue statement will affect. However, there is no harm in using the gameLoop label with the continue statement. Doing so is consistent with the label’s use alongside the break statement, and helps make the game’s logic clearer to read and understand.

>注意：
	
>如果```break```语句没有使用```gameLoop```标签，那么它将会中断```switch```代码块而不是```while```。
>使用```gameLoop```标签可以更直观的体现循环在哪里被终止的。
	
>我们还注意到，跳到下一次循环的语句：```continue gameLoop```并不一定要使用```gameLoop```标签。由于代码中只有一个循环，因此```continue```语句是没有歧义的，但是在这里使用```gameLoop```标签也是没有任何坏处的。在```break```旁边加上标签可以保证代码的一致性，是代码逻辑更清楚，更容易被人读懂和理解。





