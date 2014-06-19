# 高级操作符

除了《基础操作符》里讲到的操作符，Swift还提供了一些高级操作符，用以完成更复杂的数值运算。比如位运算和移位操作符，其语法同C和Objective-C类似。

和C语言的算术操作符不同，Swift默认不支持溢出运算。数值溢出会被捕获并报错。但是，Swift提供了另一套支持溢出运算的操作符，比如可溢出加操作符（&+），可溢出操作符都以&作为前缀。

在自定义结构体、类或者枚举类型中，可以重载Swift操作符。通过操作符重载，可以简单地实现操作符的重定义。

Swift允许用户自定义操作符，并且可定制这些操作符的优先级和结合性。


## 位操作符

位操作符可以处理数据结构中的比特位，通常在图像处理和设备驱动等底层开发程序中使用。通过位操作符，还可以有效地处理外部数据源，比如使用自定义协议进行通信时用来编解码数据。

Swift支持C语言里所有的位操作符，如下所述：

### 按位非

按位非操作符（~）对操作数每一位取反：

![按位非操作](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/bitwiseNOT_2x.png)

按位非是前置操作符，紧置于操作数之前，不带空格：

```
let initialBits: UInt8 = 0b00001111
let invertedBits = ~initialBits // 等于 11110000
```

UInt8 是8位无符号整型，可以存储0-255之间的任意数。这个例子先初始化了一个UInt8 整型变量initialBits，二进制值为00001111，前四位为0，后四位为1，换算成十进制等于15。


接着将这个变量initialBits进行按位非操作得到常量invertedBits，0变成1，1变成0，得到的二进制值为11110000，换算成十进制等于240。

### 按位与

按位与操作符（&）有两个操作数。按位与操作就是将两个操作数的每一位对齐，当对应位都是1时返回1，其他情况都返回0。

以下代码，firstSixBits 和lastSixBits 中间4个位都等于1，将它们按位与操作后得到二进制数00111100，换算成十进制为60：

```
let firstSixBits: UInt8 = 0b11111100
let lastSixBits: UInt8 = 0b00111111
let middleFourBits = firstSixBits & lastSixBits // 等于 00111100
```

### 按位或

按位或操作符（|）也有两个操作数。按位或操作就是将两个操作数的每一位对齐，当对应位有一个是1时就返回1，而只有两个位都是0的情况才返回0。

以下代码，someBits 和moreBits 在不同位上有1，将它们按位或操作后得到二进制数11111110，换算成十进制为254：

```
let someBits: UInt8 = 0b10110010
let moreBits: UInt8 = 0b01011110
let combinedbits = someBits | moreBits // 等于 11111110
```

### 按位异或

按位异或操作符（^）比较两个操作数的对应位，当两个位不同时返回1，相同时返回0。

以下代码，firstBits 和otherBits 对应位相同的情况返回0，不同的情况返回1：

```
let firstBits: UInt8 = 0b00010100
let otherBits: UInt8 = 0b00000101
let outputBits = firstBits ^ otherBits // 等于 00010001
```

## 按位左移、右移操作符

左移操作符（<<）和右移操作符（）将操作数的所有位向左或向右移动指定的位数。

按位左移和右移的效果等同于将操作数乘以或除以2的倍数。向左移动一位相当于将操作数乘以2，向右移动一位相当于将操作数除以2。


### 无符号移位操作

无符号移位的规则如下：

1.	已有的位向左或向右移动指定的位数。
2.	舍弃超出边界的位。.
3.	移动后产生的空位用0填充。

这种方法称为逻辑移位。

下图展示了11111111 << 1（11111111 左移一位）和11111111 >> 1（11111111 右移一位）的结果。蓝色数字表示被移动位，灰色表示被丢弃位，空位用橙色的0填充。

Swift移位操作代码：

```
let shiftBits: UInt8 = 4 // 即二进制的00000100
shiftBits << 1 // 00001000
shiftBits << 2 // 00010000
shiftBits << 5 // 10000000
shiftBits << 6 // 00000000
shiftBits >> 2 // 00000001
```

移位操作可以对其他数据类型实现编码和解码：

```
let pink: UInt32 = 0xCC6699
let redComponent = (pink & 0xFF0000) >> 16 // redComponent是0xCC, 即204
let greenComponent = (pink & 0x00FF00) >> 8 // greenComponent是0x66, 即102
let blueComponent = pink & 0x0000FF // blueComponent是0x99, 即153
```

这个例子中用一个UInt32 常量pink 来存储css中粉色的颜色值。CSS中颜色#CC6699在Swift用十六进制0xCC6699来表示。这个颜色值经过按位与（&）和按位右移操作后可分解出它的红色成分（CC）、绿色成分（66）和蓝色成分（99）。

对0xCC6699 和0xFF0000进行按位与操作就可以得到红色成分。0xFF0000 里的0类似于遮罩，将0xCC6699的第二和第三字节过滤掉后返回0xCC0000 。

然后，将0xCC0000 向右移动16位。因为十六进制中每两个字符占8个比特位，所以移动16位的结果是把0xCC0000 变成0x0000CC，等同于0xCC，换算成十进制是204。

同理，对0xCC6699 和0x00FF00进行按位与操作可以得到绿色成分。将结果值0x006600再向右移动8位得到0x66，换算成十进制是102。

最后，对0xCC6699 和0x0000FF进行按位与操作可以得到蓝色成分。结果值0x000099不需要再做移位操作，因为0x000099 等价于0x99，换算成十进制是153。

### 有符号移位操作

有符号的移位操作相对复杂得多，因为正负号也是用二进制位表示的。(下面举的例子虽然都是8位的，但原理是通用的。)

有符号整型的第一位为符号位，0代表正数，1代表负数，其余的为数值位。有符号和无符号正整数的存储结构是相同的，比如数值4的二进制结构图：

符号位为0，代表正数，其余7个数值位用二进制表示十进制的4。

负数的存储不太一样，它存储的是2的n次方减去它的绝对值，n为数值位的位数。比如一个8位的数有7个数值位，所以是2的7次方，即128。我们来看下数值-4的二进制结构图：

这里符号位为1，代表负数，其余7个数值位的值是124（即128-4）：

负数的编码方式称为二进制补码表示。这种表示方式看起来很奇怪，但它有几个优点。

首先，对全部8个比特位(包括符号位)做标准的二进制加法就可以完成-1 加 -4 的操作，加法过程中丢弃超出的比特位。

第二，使用二进制补码表示方式，我们可以和正数一样对负数进行按位左移或右移，同样也是左移1位时乘于2，右移1位时除于2。但是，对有符号整型的右移有一个特别的要求：

+ 有符号和无符号整型按位右移时规则相同，但有符号整型移位后出现的空位使用符号位来填充，而不是0。

这就确保了按位右移后，有符号整型的符号不会发生变化。这称为算术移位。

因为正数和负数特殊的存储方式，向右移位都会使它们更接近于0。移位过程中保持符号位不变，所以负数向右移位时值虽然接近于0但始终是负数。

## 溢出操作符

当给整型常量或变量赋值溢出时，Swift默认会报错，这就保证了操作过大或过小数据时的安全性。

举个例子，Int16整型能表示-32768 到 32767之间任意的有符号整数，但如果给它 赋值超出该范围则会导致错误：

```
var potentialOverflow = Int16.max
// potentialOverflow 等于 32767, 即Int16能表示的最大值
potentialOverflow += 1
// 噢，出错了
```

值溢出时提供错误处理机制可以使编程更灵活。

然而，需要判断溢出条件时，你可以采用溢出运算，而不是触发错误。Swfit为整型计算提供了5个以&符号开头的溢出操作符。

+ 溢出加法(&+)
+ 溢出减法(&-)
+ 溢出乘法(&*)
+ 溢出除法(&/)
+ 溢出取余(&%)

### 上溢出

下面的例子展示了溢出加法(&+)的用法：

```
var willOverflow = UInt8.max
// willOverflow 等于 255, 即UInt8 能表示的最大值
willOverflow = willOverflow &+ 1
// 现在willOverflow 等于 0
```

willOverflow 等于UInt8 所能表示的最大值255(二进制11111111)，使用溢出加法&+加1，如下图所示因为上溢出UInt8 无法表示出这个新值了。溢出后，有效位为00000000，也就是0。

### 下溢出

数值也有可能因为太小而越界。举个例子：

UInt8能表示的最小值是0(二进制为00000000)。对00000000使用溢出减法&-减1，就会得到二进制数11111111，即十进制的255。

代码如下：

```
var willUnderflow = UInt8.min
// willUnderflow 等于 0, 即UInt8能表示的最小值
willUnderflow = willUnderflow &- 1
// 现在willUnderflow 等于255
```

有符号整型也有类似的下溢出，它所有的减法都是对包括符号位在内的二进制数进行二进制减法，这在 "按位左移、右移操作符" 一节提到过。Int8 能表示的最小整数是-128，即二进制的10000000。用溢出减法减去1后，变成了01111111，即Int8 能表示的最大整数127。

代码如下：

```
var signedUnderflow = Int8.min
// signedUnderflow 等于 -128, 即Int8 能表示的最小值
signedUnderflow = signedUnderflow &- 1
// 现在signedUnderflow 等于 127
```

有符号和无符号整型的上溢出总是从最大有效值变成最小值，下溢出总是从最小有效值变成最大值。

### 除零溢出

将一个数除以0或者对0取余都会导致错误：

```
let x = 1
let y = x / 0
```

但是使用可溢出版本的操作符&/和&%会返回0值。

```
let x = 1
let y = x &/ 0
// y 等于 0
```

## 优先级和结合性

操作符的优先级有高低之分，高优先级的操作符会先被计算。

结合性规定了具有相同优先级的操作符如何分组——向左还是向右。意思就是，到底是和左边的表达式结合，还是和右边的表达式结合。

在复合表达式中，操作符的优先级和结合性是非常重要的。举个例子，为什么下列表达式的结果为4？

```
2 + 3 * 4 % 5
// 结果等于 4
```

如果严格地从左到右计算，计算过程会是这样：

+ 2 + 3 = 5;
+ t 5 * 4 = 20;
+ 20 %5 = 0

但是正确答案是4而不是0。优先级高的操作符要先计算，在Swift和C语言中，都是先乘除后加减的。所以，执行完乘法和取余运算才能执行加法运算。

乘法和取余拥有相同的优先级，在运算过程中，我们还需要考虑结合性。乘法和取余运算都是左结合的。这相当于在表达式中有隐藏的括号让运算从左开始：

```
2 + ((3 * 4) % 5)
```

(3 * 4)等于 12,相当于

```
2 + (12 % 5)
```

(12 % 5) 等于 2，相当于

```
2 + 2
```

最后计算结果为 4。

Swift操作符的优先级和结合性的完整规则，请看表达式。

> <b>注意：</b>
>
> Swift操作符的优先级和结合性的规则跟C系语言不太一样，相对于C语言和Objective-C更加简单且保守。所以在移植已有代码到Swift时，注意确认操作数的计算顺序。

## 操作符函数

类和结构体重新自定义已有操作符的功能，这称为操作符重载。

下面的例子展示了一个自定义结构体的加法运算。加操作符是一个二元操作符，因为它有两个操作数，而且是中置操作符，必须出现在两个操作数之间。

例子中定义了一个名为Vector2D 的结构体，表示二维坐标向量(x, y)。随后定义了Vector2D 实例对象相加的操作符函数。

```
struct Vector2D {
	var x = 0.0, y = 0.0
}
@infix func + (left: Vector2D, right: Vector2D) -> Vector2D {
	return Vector2D(x: left.x + right.x, y: left.y + right.y)
}
```

该操作符函数定义了一个全局的+函数，参数是两个Vector2D 类型的实例，返回值也是一个Vector2D 类型。函数声明中，在关键字fun之前用@infix 属性定义一个中置操作符。

在这个代码实现中，参数被命名为left和right，代表+左边和右边的两个Vector2D对象。函数返回了一个新的Vector2D对象，这个对象的x和y分别等于两个参数对象的x和y的和。

这个函数是全局的，而不是Vector2D结构的成员方法，所以任意两个Vector2D对象都可以使用这个中置运算符：

```
let vector = Vector2D(x: 3.0, y: 1.0)
let anotherVector = Vector2D(x: 2.0, y: 4.0)
let combinedVector = vector + anotherVector
// combinedVector 是一个Vector2D 实例 ，值为(5.0, 5.0)
```

这个例子将向量 (3.0，1.0) 和 (2.0，4.0) 相加，得到向量 (5.0，5.0)，如下图所示：

## 前置和后置操作符

上个例子演示了一个二元中置操作符的自定义实现，同样类和结构体也可以重载标准的一元操作符。一元操作符只有一个操作数，在操作数之前为前置操作符（比如-a），在操作数之后为后置操作符（比如i++）。

函数声明中，在关键字fun之前用@ prefix 属性定义前置操作符，@postfix 定义后置操作符。

```
@prefix func - (vector: Vector2D) -> Vector2D {
  return Vector2D(x: -vector.x, y: -vector.y)
}
```

这段代码实现了Vector2D对象的一元减操作符(-a)，@prefix表明它是前置的。

对于数值，一元减操作符可以把正数变负数，把负数变正数。对于Vector2D对象，一元减操作符将其x和y都进行一元减运算。

```
let positive = Vector2D(x: 3.0, y: 4.0)
let negative = -positive
// negative 是 Vector2D实例，值为(-3.0, -4.0)
let alsoPositive = -negative
// alsoPositive 也是 Vector2D实例，值为(3.0, 4.0)
```

## 复合赋值操作符

复合赋值是其他操作符和赋值操作符一起执行的运算。如+=把加运算和赋值运算组合成一个操作。实现一个复合赋值操作符需要使用@assignment属性，操作符左边的参数作为函数输入，函数内再修改它的值。

下面的例子实现了Vector2D 对象的+=操作符：

```
@assignment func += (inout left: Vector2D, right: Vector2D) {
	left = left + right
}
```

加法运算之前定义过了，这里无需重新定义。加赋操作符函数使用已有的加法运算将左值加上右值：

```
var original = Vector2D(x: 1.0, y: 2.0)
let vectorToAdd = Vector2D(x: 3.0, y: 4.0)
original += vectorToAdd
// 运算后original 等于 (4.0, 6.0)
```

可以将 @assignment 属性和 @prefix 或 @postfix 属性组合起来，比如像下面Vector2D对象的前置运算符(++a)：

```
@prefix @assignment func ++ (inout vector: Vector2D) -> Vector2D {
	vector += Vector2D(x: 1.0, y: 1.0)
	return vector
}
```

这个自加操作符函数使用了前面定义过的加赋运算，将自己加上一个值为 (1.0，1.0) 的对象然后将返回值赋给自己。

```
var toIncrement = Vector2D(x: 3.0, y: 4.0)
let afterIncrement = ++toIncrement
// toIncrement 等于(4.0, 5.0)
// afterIncrement 也等于 (4.0, 5.0)
```

> <b>注意：</b>
>
> 默认的赋值符(=)是不可重载的。只有复合赋值符可以重载。条件操作符 a？b：c 也是不可重载的。

## 比较操作符

自定义的类和结构体默认没有相等(==)和不等(!=)操作符，因为Swift无法知道自定义类型怎样算相等，怎样算不等。

定义相等操作符跟定义其他中置操作符类似：

```
@infix func == (left: Vector2D, right: Vector2D) -> Bool {
	return (left.x == right.x) && (left.y == right.y)
}
@infix func != (left: Vector2D, right: Vector2D) -> Bool {
	return !(left == right)
}
```

上述代码实现了相等操作符==来判断两个Vector2D对象是否相等，相等的概念就是它们有相同的x值和y值。将相等操作符==的结果取反就实现了不等运算符!=。

现在我们可以使用这两个操作符来判断两个Vector2D对象是否相等。

```
let twoThree = Vector2D(x: 2.0, y: 3.0)
let anotherTwoThree = Vector2D(x: 2.0, y: 3.0)
if twoThree == anotherTwoThree {
println("这两个向量相等")
}
// 输出结果 "这两个向量相等"
```

## 自定义操作符

除了标准的操作符，你还可以声明一些个性的操作符，但自定义操作符只能使用这些字符/ = - + * % < >！& | ^。~。

新的操作符需要在全局域使用operator关键字声明，可以声明为前置，中置或后置的。

```
operator prefix +++ {}
```

这段代码定义了一个新的前置操作符+++，此前Swift并不存在这个操作符，此处针对Vector2D 对象的这个操作符具有个性化的含义。+++被定义为 双自增 操作符，它使用之前定义的加赋运算将自已加上自己然后返回。

```
@prefix @assignment func +++ (inout vector: Vector2D) -> Vector2D {
vector += vector
return vector
}
```

Vector2D 的 +++ 和 ++ 很类似, 唯一不同的是前者加自己, 后者是加值为 (1.0, 1.0) 的向量。

```
var toBeDoubled = Vector2D(x: 1.0, y: 4.0)
let afterDoubling = +++toBeDoubled
// toBeDoubled 等于 (2.0, 8.0)
// afterDoubling 也等于 (2.0, 8.0)
```

## 自定义中置操作符的优先级和结合性

可以为自定义的中置操作符指定优先级和结合性。可以回头看看优先级和结合性中解释的，这两个因素是如何影响复合表达式的求值顺序的。

结合性有left，right和none三种情况。左结合操作符跟其他优先级相同的左结合操作符写在一起时，会跟左边的操作数结合。同理，右结合操作符会跟右边的操作数结合。而非结合操作符不能跟其他优先级相同的操作符写在一起。

结合性默认为none，优先级默认为100。

下面的例子定义了一个左结合且优先级为140的中置操作符+-。

```
operator infix +- { associativity left precedence 140 }
func +- (left: Vector2D, right: Vector2D) -> Vector2D {
	return Vector2D(x: left.x + right.x, y: left.y - right.y)
}
let firstVector = Vector2D(x: 1.0, y: 2.0)
let secondVector = Vector2D(x: 3.0, y: 4.0)
let plusMinusVector = firstVector +- secondVector
// plusMinusVector 是 Vector2D实例，等于 (4.0, -2.0)
```

这个操作符把两个向量的x相加， y相减。因为它实际上属于加减运算，所以让它保持了和加减法一样的结合性和优先级(左结合，优先级为140)。查阅完整的Swift默认优先级和结合性的设置，请移步表达式;





