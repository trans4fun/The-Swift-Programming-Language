#Summary of the Grammar
#语法总结

##Statements
##语句

###GRAMMAR OF A STATEMENT

‌ statement → expression;opt

‌ statement → declaration;opt

‌ statement → loop-statement;opt

‌ statement → branch-statement;opt

‌ statement → labeled-statement

‌ statement → control-transfer-statement;opt

‌ statements → statementstatements opt

###语句语法
语句 → 表达式 ;可选

语句 → 声明 ;可选

语句 → 循环语句 ;可选

语句 → 分支语句 ;可选

语句 → 标记语句

语句 → 控制转移语句 ;可选

多条语句 → 语句 多条语句 可选

###GRAMMAR OF A LOOP STATEMENT

‌ loop-statement → for-statement

‌ loop-statement → for-in-statement

‌ loop-statement → while-statement

‌ loop-statement → do-while-statement

###循环语句语法
循环语句 → for 语句

循环语句 → for in 语句

循环语句 → while 语句

循环语句 → do-while 语句

###GRAMMAR OF A FOR STATEMENT

‌ for-statement → for for-init opt ;expression opt ; expression opt code-block

‌ for-statement → for (for-init opt ;expression opt ; expression opt) code-block

‌ for-init → variable-declaration  expression-list

###for 语句语法
for语句 → **for** for-初始条件 可选; 表达式 可选 ;表达式 可选 代码块

for语句 → **for** ( for-初始条件 可选; 表达式 可选 ;表达式 可选 ) 代码块

for-初始条件 → 变量声明 | 表达式列表

###GRAMMAR OF A FOR-IN STATEMENT

‌ for-in-statement → **for** pattern **in** expression code-block

###for-in 语句语法
for-in 语句 → for 模式 in 表达式代码块

###GRAMMAR OF A WHILE STATEMENT

‌ while-statement → while while-condition code-block

‌ while-condition → expression  declaration

###while 语句语法
while语句 → **while** while-条件 代码块

while-条件 → 表达式 | 声明

###GRAMMAR OF A DO-WHILE STATEMENT

‌ do-while-statement → do code-block while while-condition

###do-while 语句语法
do-while语句 → **do** 代码块 **while** while-条件


###GRAMMAR OF A BRANCH STATEMENT

‌ branch-statement → if-statement

‌ branch-statement → switch-statement

###分支语句语法

分支语句 → if语句

分支语句 → switch语句

###GRAMMAR OF AN IF STATEMENT

‌ if-statement → **if** if-condition code-block else-clause opt

‌ if-condition → expression | declaration

‌ else-clause → **else** code-block  | **else** if-statement

###if 语句语法
if语句 → if if-条件 代码块 else 子句 可选

if条件 → 表达式 | 申明

else子句 → else 代码块 | else if-语句

###GRAMMAR OF A SWITCH STATEMENT

‌ switch-statement → switch expression{switch-casesopt}

‌ switch-cases → switch-case switch-cases opt

‌ switch-case → case-label statements | default-label statements

‌ switch-case → case-label;  | default-label;

‌ case-label → case case-item-list:

‌ case-item-list → patternguard-clause opt | pattern guard-clause opt,case-item-list

‌ default-label → default:

‌ guard-clause → whereguard-expression

‌ guard-expression → expression

###switch语句语法
switch语句 → **switch** 表达式 { switch-case列表 可选 }

switch-case列表 → switch-case switch-case列表 可选

switch-case → case标签 多条语句 | default标签 多条语句

switch-case → case标签 ; | default标签 ;

case标签 → **case** case项列表 :

case项列表 → 模式 监护子句 可选 | 模式 监护子句 可选 , case项列表

default标签 → **default** :

监护字句 → **where** 监护表达式

监护表达式 → 表达式

###GRAMMAR OF A LABELED STATEMENT

‌ labeled-statement → statement-label loop-statement | statement-label switch-statement

‌ statement-label → label-name:

‌ label-name → identifier

###标记语句语法
标记语句 → 语句标签 循环语句 | 语句标签 switch语句

语句标签 → 标签名称 :

标签名称 → 标识符

###GRAMMAR OF A CONTROL TRANSFER STATEMENT

‌ control-transfer-statement → break-statement

‌ control-transfer-statement → continue-statement

‌ control-transfer-statement → fallthrough-statement

‌ control-transfer-statement → return-statement

###控制传递语句语法
控制传递语句 → break-语句

控制传递语句 → continue-语句

控制传递语句 → fallthrough-语句

控制传递语句 → return-语句

###GRAMMAR OF A BREAK STATEMENT

‌ break-statement → breaklabel-name opt

###break 语句语法
break语句 → **break** 标签名称 可选


###GRAMMAR OF A CONTINUE STATEMENT

‌ continue-statement → continue label-name opt

###continue 语句语法
continue语句 → **continue** 标签名称 可选

###GRAMMAR OF A FALLTHROUGH STATEMENT

‌ fallthrough-statement → fallthrough

###fallthrough 语句语法
fallthrough-语句 → **fallthrough**

###GRAMMAR OF A RETURN STATEMENT

‌ return-statement → return expression opt
####return 语句语法
return语句 → **return** 表达式 可选

##Generic Parameters and Arguments


##泛型和参数

###GRAMMAR OF A GENERIC PARAMETER CLAUSE

‌ generic-parameter-clause → <generic-parameter-list requirement-clause opt>

‌ generic-parameter-list → generic-parameter | generic-parameter,generic-parameter-list

‌ generic-parameter → type-name

‌ generic-parameter → type-name:type-identifier

‌ generic-parameter → type-name:protocol-composition-type

‌ requirement-clause → where requirement-list

‌ requirement-list → requirement | requirement,requirement-list

‌ requirement → conformance-requirement  | same-type-requirement

‌ conformance-requirement → type-identifier:type-identifier

‌ conformance-requirement → type-identifier:protocol-composition-type

‌ same-type-requirement → type-identifier==type-identifier

###泛型形参子句语法 

泛型参数子句 → < 泛型参数列表 约束子句 可选 >

泛型参数列表 → 泛形参数 | 泛形参数 , 泛型参数列表

泛形参数 → 类型名称

泛形参数 → 类型名称 : 类型标识

泛形参数 → 类型名称 : 协议合成类型

约束子句 → **where** 约束列表

约束列表 → 约束 | 约束 , 约束列表

约束 → 一致性约束 | 同类型约束

一致性约束 → 类型标识 : 类型标识

一致性约束 → 类型标识 : 协议合成类型

同类型约束 → 类型标识 == 类型标识

###GRAMMAR OF A GENERIC ARGUMENT CLAUSE

‌ generic-argument-clause → <generic-argument-list>

‌ generic-argument-list → generic-argument | generic-argument,generic-argument-list

‌ generic-argument → type

###泛型参数子句语法
泛型参数子句 → < 泛型参数列表 >

泛型参数列表 → 泛型参数 | 泛型参数 , 泛型参数列表

泛型参数 → 类型

##Declarations
##声明
###GRAMMAR OF A DECLARATION

‌ declaration → import-declaration

‌ declaration → constant-declaration

‌ declaration → variable-declaration

‌ declaration → typealias-declaration

‌ declaration → function-declaration

‌ declaration → enum-declaration

‌ declaration → struct-declaration

‌ declaration → class-declaration

‌ declaration → protocol-declaration

‌ declaration → initializer-declaration

‌ declaration → deinitializer-declaration

‌ declaration → extension-declaration

‌ declaration → subscript-declaration

‌ declaration → operator-declaration

‌ declarations → declarationdeclarations opt

‌ declaration-specifiers → declaration-specifier declaration-specifiersopt

‌ declaration-specifier → class | mutating | nonmutating |  override | static | unowned |  unowned(safe) | unowned(unsafe) | weak


###声明语法

声明 → 导入声明

声明 → 常量声明

声明 → 变量声明

声明 → 类型别名声明

声明 → 函数声明

声明 → 枚举声明

声明 → 结构体声明

声明 → 类声明

声明 → 协议声明

声明 → 构造器声明

声明 → 析构器声明

声明 → 扩展声明

声明 → 下标脚本声明

声明 → 运算符声明

声明列表 → 声明 声明列表 可选

声明描述符列表 → 声明描述符 声明描述符列表 可选

声明描述符 → **class** | **mutating** | **nonmutating** | **override** | **static** | **unowned** | **unowned(safe) **| **unowned(unsafe)** | **weak**

###GRAMMAR OF A TOP-LEVEL DECLARATION

‌ top-level-declaration → statements opt

###顶级声明语法
顶级声明 → 多条语句 可选

###GRAMMAR OF A CODE BLOCK

‌ code-block → {statements opt}

###代码块语法
代码块 → { 多条语句 可选 }

###GRAMMAR OF AN IMPORT DECLARATION

‌ import-declaration → attributes opt import import-kind opt import-path

‌ import-kind → typealias | struct | class | enum | protocol | var | func

‌ import-path → import-path-identifier |  import-path-identifier.import-path

‌ import-path-identifier → identifier |  operator

###导入声明语法
导入声明 → 属性列表 可选 **import** 导入类型 可选 导入路径

导入类型 → **typealias** | **struct** | **class** | **enum** | **protocol** | **var** | **func**

导入路径 → 导入路径标识符 | 导入路径标识符 . 导入路径

导入路径标识符 → 标识符 | 运算符

###GRAMMAR OF A CONSTANT DECLARATION

‌ constant-declaration → attributes opt declaration-specifiers opt let pattern-initializer-list

‌ pattern-initializer-list → pattern-initializer |  pattern-initializer,pattern-initializer-list

‌ pattern-initializer → pattern initializer opt

‌ initializer → =expression

###常数声明语法
常量声明 → 属性列表 可选 声明描述符列表 可选 **let** 模式构造器列表

模式构造器列表 → 模式构造器 | 模式构造器 , 模式构造器列表

模式构造器 → 模式 构造器 可选

构造器 → = 表达式

###GRAMMAR OF A VARIABLE DECLARATION

‌ variable-declaration → variable-declaration-head pattern-initializer-list

‌ variable-declaration → variable-declaration-head variable-name type-annotationcode-block

‌ variable-declaration → variable-declaration-head variable-name type-annotation getter-setter-block

‌ variable-declaration → variable-declaration-head variable-name type-annotation getter-setter-keyword-block

‌ variable-declaration → variable-declaration-head variable-name type-annotation initializer opt willSet-didSet-block

‌ variable-declaration-head → attributes opt declaration-specifiers opt var

‌ variable-name → identifier

‌ getter-setter-block → {getter-clausesetter-clauseopt}

‌ getter-setter-block → {setter-clausegetter-clause}

‌ getter-clause → attributes opt getcode-block

‌ setter-clause → attributes opt setsetter-nameoptcode-block

‌ setter-name → (identifier)

‌ getter-setter-keyword-block → {getter-keyword-clausesetter-keyword-clauseopt}

‌ getter-setter-keyword-block → {setter-keyword-clausegetter-keyword-clause}

‌ getter-keyword-clause → attributes opt get

‌ setter-keyword-clause → attributes opt set

‌ willSet-didSet-block → {willSet-clausedidSet-clauseopt}

‌ willSet-didSet-block → {didSet-clausewillSet-clause}

‌ willSet-clause → attributes opt willSetsetter-name opt code-block

‌ didSet-clause → attributes opt didSetsetter-name opt code-block

###变量声明语法
变量声明 → 变量声明头 模式构造器列表

变量声明 → 变量声明头 变量名 类型注解 代码块

变量声明 → 变量声明头 变量名 类型注解 getter-setter块

变量声明 → 变量声明头 变量名 类型注解 getter-setter关键字块

变量声明 → 变量声明头 变量名 类型注解 构造器 可选 willSet-didSet代码块

变量声明头 → 属性列表 可选 声明描述符列表 可选 **var**

变量名称 → 标识符

getter-setter块 → { getter子句 setter子句 可选 }

getter-setter块 → { setter子句 getter子句 }

getter子句 → 属性列表 可选 **get** 代码块

setter子句 → 属性列表 可选 **set** setter名称 可选 代码块

setter名称 → **(** 标识符 **)**

getter-setter关键字块 → **{** getter关键字子句 setter关键字子句 可选 **}**

getter-setter关键字块 → **{ **setter关键字子句 getter关键字子句 **}**

getter关键字子句 → 属性列表 可选 **get**

setter关键字子句 → 属性列表 可选 **set**

willSet-didSet代码块 → **{** willSet子句 didSet子句 可选**}**

willSet-didSet代码块 → **{** didSet子句 willSet子句 **}**

willSet子句 → 属性列表 可选 **willSet** setter名称 可选 代码块

didSet子句 → 属性列表 可选 **didSet** setter名称 可选 代码块

###GRAMMAR OF A TYPE ALIAS DECLARATION

‌ typealias-declaration → typealias-head typealias-assignment

‌ typealias-head → typealias typealias-name

‌ typealias-name → identifier

‌ typealias-assignment → =type

###类型别名声明语法

类型别名声明 → 类型别名头 类型别名赋值

类型别名头 → **typealias** 类型别名名称

类型别名名称 → 标识符

类型别名赋值 → = 类型


###GRAMMAR OF A FUNCTION DECLARATION

‌ function-declaration → function-head function-name generic-parameter-clause opt function-signature function-body

‌ function-head → attributes opt declaration-specifiers opt func

‌ function-name → identifier | operator

‌ function-signature → parameter-clauses function-result opt

‌ function-result → ->attributes opt type

‌ function-body → code-block

‌ parameter-clauses → parameter-clauseparameter-clauses opt

‌ parameter-clause → () | (parameter-list...opt)

‌ parameter-list → parameter | parameter,parameter-list

‌ parameter → inout opt let opt # opt parameter-name local-parameter-name opt type-annotation default-argument-clause opt

‌ parameter → inout opt var# opt parameter-name local-parameter-name opt type-annotation default-argument-clause opt

‌ parameter → attributes opt type

‌ parameter-name → identifier |  _

‌ local-parameter-name → identifier | _

‌ default-argument-clause → =expression

###函数声明语法
函数声明 → 函数头 函数名 泛型参数子句 可选 函数签名 函数体

函数头 → 属性列表 可选 声明描述符列表 可选 **func**

函数名 → 标识符 | 运算符

函数签名 → 参数子句列表 函数结果 可选

函数结果 → → 属性列表 可选 类型

函数体 → 代码块

参数子句列表 → 参数子句 参数子句列表 可选

参数子句 → **( ) **| ( 参数列表 ... 可选 )

参数列表 → 参数 | 参数 , 参数列表

参数 → **inout** 可选 **let** 可选 **#** 可选 参数名 局部参数名 可选 类型注解 默认参数子句 可选

参数 → **inout** 可选 **var** **#** 可选 参数名 局部参数名 可选 类型注解 默认参数子句 可选

参数 → 属性列表 可选 类型

参数名 → 标识符 | _

局部参数名 → 标识符 | _

默认参数子句 → = 表达式

###GRAMMAR OF AN ENUMERATION DECLARATION

‌ enum-declaration → attributes opt union-style-enum | attributes opt raw-value-style-enum

‌ union-style-enum → enum-name generic-parameter-clause opt { union-style-enum-members opt }

‌ union-style-enum-members → union-style-enum-member union-style-enum-members opt

‌ union-style-enum-member → declaration | union-style-enum-case-clause

‌ union-style-enum-case-clause → attributes opt case union-style-enum-case-list

‌ union-style-enum-case-list → union-style-enum-case | union-style-enum-case,union-style-enum-case-list

‌ union-style-enum-case → enum-case-nametuple-type opt

‌ enum-name → identifier

‌ enum-case-name → identifier

‌ raw-value-style-enum → enum-name generic-parameter-clause opt:type-identifier{raw-value-style-enum-members opt}

‌ raw-value-style-enum-members → raw-value-style-enum-member raw-value-style-enum-members opt

‌ raw-value-style-enum-member → declaration  raw-value-style-enum-case-clause

‌ raw-value-style-enum-case-clause → attributes opt caseraw-value-style-enum-case-list

‌ raw-value-style-enum-case-list → raw-value-style-enum-case raw-value-style-enum-case,raw-value-style-enum-case-list

‌ raw-value-style-enum-case → enum-case-name raw-value-assignment opt

‌ raw-value-assignment → =literal


###枚举声明语法
枚举声明 → 属性列表 可选 联合式枚举 | 属性列表 可选 原始值式枚举

联合式枚举 → 枚举名 泛型参数子句 可选 { union-style-enum-members 可选 }

union-style-enum-members → union-style-enum-member union-style-enum-members 可选

union-style-enum-member → 声明 | 联合式的枚举case子句

联合式的枚举case子句 → 属性列表 可选 **case** 联合式的枚举case列表

联合式的枚举case列表 → 联合式的case | 联合式的case , 联合式的枚举case列表

联合式的case → 枚举的case名 元组类型 可选

枚举名 → 标识符

枚举的case名 → 标识符

原始值式枚举 → 枚举名 泛型参数子句 可选 : 类型标识 { 原始值式枚举成员列表 可选 }

原始值式枚举成员列表 → 原始值式枚举成员 原始值式枚举成员列表 可选

原始值式枚举成员 → 声明 | 原始值式枚举case子句

原始值式枚举case子句 → 属性列表 可选 **case** 原始值式枚举case列表

原始值式枚举case列表 → 原始值式枚举case | 原始值式枚举case , 原始值式枚举case列表

原始值式枚举case → 枚举的case名 原始值赋值 可选

原始值赋值 → = 字面量

###GRAMMAR OF A STRUCTURE DECLARATION

‌ struct-declaration → attributes opt struct struct-name generic-parameter-clause opt type-inheritance-clause opt struct-body

‌ struct-name → identifier

‌ struct-body → {declarations opt}
###结构体声明语法
结构体声明 → 属性列表 可选 **struct** 结构体名称 泛型参数子句 可选 类型继承子句 可选 结构体主体

结构体名称 → 标识符

结构体主体 → { 声明列表 可选 }

###GRAMMAR OF A CLASS DECLARATION

‌ class-declaration → attributes opt classclass-name generic-parameter-clause opt type-inheritance-clause opt class-body

‌ class-name → identifier

‌ class-body → {declarations opt}

###类声明语法
类声明 → 属性列表 可选 class 类名 泛型参数子句 可选 类型继承子句 可选 类主体

类名 → 标识符

类主体 → { 声明列表 可选 }


###GRAMMAR OF A PROTOCOL DECLARATION

‌ protocol-declaration → attributes opt protocol protocol-name type-inheritance-clause opt protocol-body

‌ protocol-name → identifier

‌ protocol-body → {protocol-member-declarations opt}

‌ protocol-member-declaration → protocol-property-declaration

‌ protocol-member-declaration → protocol-method-declaration

‌ protocol-member-declaration → protocol-initializer-declaration

‌ protocol-member-declaration → protocol-subscript-declaration

‌ protocol-member-declaration → protocol-associated-type-declaration

‌ protocol-member-declarations → protocol-member-declarationprotocol-member-declarations opt


###协议声明语法
协议声明 → 属性列表 可选 **protocol** 协议名 类型继承子句 可选 协议主体

协议名 → 标识符

协议主体 → { 协议成员声明列表 可选 }

协议成员声明 → 协议属性声明

协议成员声明 → 协议方法声明

协议成员声明 → 协议构造器声明

协议成员声明 → 协议下标脚本声明

协议成员声明 → 协议关联类型声明

协议成员声明列表 → 协议成员声明 协议成员声明列表 可选

###GRAMMAR OF A PROTOCOL PROPERTY DECLARATION

‌ protocol-property-declaration → variable-declaration-head variable-name type-annotation getter-setter-keyword-block

###协议属性声明语法
协议属性声明 → 变量声明头 变量名 类型注解 getter-setter关键字块

###GRAMMAR OF A PROTOCOL METHOD DECLARATION

‌ protocol-method-declaration → function-head function-namem generic-parameter-clause opt function-signature

###协议方法声明语法
协议方法声明 → 函数头 函数名 泛型参数子句 可选 函数签名


###GRAMMAR OF A PROTOCOL INITIALIZER DECLARATION

‌ protocol-initializer-declaration → initializer-head generic-parameter-clause opt parameter-clause

###协议构造器声明语法
协议构造器声明 → 构造器头 泛型参数子句 可选 参数子句

###GRAMMAR OF A PROTOCOL SUBSCRIPT DECLARATION

‌ protocol-subscript-declaration → subscript-head subscript-result getter-setter-keyword-block

###协议下标脚本声明语法
协议下标脚本声明 → 下标脚本头 下标脚本结果 getter-setter关键字块

###GRAMMAR OF A PROTOCOL ASSOCIATED TYPE DECLARATION

‌ protocol-associated-type-declaration → typealias-head type-inheritance-clause opt typealias-assignment opt

###协议关联类型声明语法
协议关联类型声明 → 类型别名头 类型继承子句 可选 类型别名赋值 可选


###GRAMMAR OF AN INITIALIZER DECLARATION

‌ initializer-declaration → initializer-head generic-parameter-clause opt parameter-clause initializer-body

‌ initializer-head → attributes opt convenience opt init

‌ initializer-body → code-block

###构造器声明语法

构造器声明 → 构造器头 泛型参数子句 可选 参数子句 构造器主体

构造器头 → 属性列表 可选 **convenience** 可选 **init**

构造器主体 → 代码块

###GRAMMAR OF A DEINITIALIZER DECLARATION

‌ deinitializer-declaration → attributes opt deinitcode-block

###析构器声明语法

析构器声明 → 属性列表 可选 **deinit** 代码块

###GRAMMAR OF AN EXTENSION DECLARATION

‌ extension-declaration → extensiontype-identifiertype-inheritance-clause opt extension-body

‌ extension-body → {declarations opt}

###扩展声明语法
扩展声明 → **extension** 类型标识 类型继承子句 可选 extension-主体

extension-主体 → { 声明列表 可选 }

###GRAMMAR OF A SUBSCRIPT DECLARATION

‌ subscript-declaration → subscript-head subscript-result code-block

‌ subscript-declaration → subscript-head subscript-result getter-setter-block

‌ subscript-declaration → subscript-head subscript-result getter-setter-keyword-block

‌ subscript-head → attributes opt subscript parameter-clause

‌ subscript-result → ->attributesopttype

###下标脚本声明语法
下标脚本声明 → 下标脚本头 下标脚本结果 代码块

下标脚本声明 → 下标脚本头 下标脚本结果 getter-setter块

下标脚本声明 → 下标脚本头 下标脚本结果 getter-setter关键字块

下标脚本头 → 属性列表 可选 下表脚本参数子句

下标脚本结果 → → 属性列表 可选 类型

###GRAMMAR OF AN OPERATOR DECLARATION

‌ operator-declaration → prefix-operator-declaration | postfix-operator-declaration | infix-operator-declaration

‌ prefix-operator-declaration → operator prefix operator{}

‌ postfix-operator-declaration → operator postfix operator{}

‌ infix-operator-declaration → operator infix operator{infix-operator-attributes opt}

‌ infix-operator-attributes → precedence-clause opt associativity-clause opt

‌ precedence-clause → precedence precedence-level

‌ precedence-level → Digit 0 through 255

‌ associativity-clause → associativity associativity

‌ associativity → left  right  none

###运算符声明语法
运算符声明 → 前置运算符声明 | 后置运算符声明 | 中置运算符声明

前置运算符声明 → **operator prefix** 运算符 { }

后置运算符声明 → **operator postfix** 运算符 { }

中置运算符声明 → **operator infix** 运算符 { 中置运算符属性 可选 }

中置运算符属性 → 优先级子句 可选 结和性子句 可选

优先级子句 → **precedence** 优先级水平

优先级水平 → 数值 0 到 255

结和性子句 → **associativity** 结和性

结和性 → **left** | **right** | **none**

##Patterns
##模式

###GRAMMAR OF A PATTERN

‌ pattern → wildcard-patterntype-annotation opt

‌ pattern → identifier-patterntype-annotation opt

‌ pattern → value-binding-pattern

‌ pattern → tuple-patterntype-annotation opt

‌ pattern → enum-case-pattern

‌ pattern → type-casting-pattern

‌ pattern → expression-pattern

###模式语法

模式 → 通配符模式 类型注解 可选

模式 → 标识符模式 类型注解 可选

模式 → 值绑定模式

模式 → 元组模式 类型注解 可选

模式 → 枚举用例模式

模式 → 类型转换模式

模式 → 表达式模式

###GRAMMAR OF A WILDCARD PATTERN

‌ wildcard-pattern → _

###通配符模式语法

通配符模式 → **_**

###GRAMMAR OF AN IDENTIFIER PATTERN

‌ identifier-pattern → identifier

###标识符模式语法
标识符模式 → 标识符

###GRAMMAR OF A VALUE-BINDING PATTERN

‌ value-binding-pattern → varpattern  let pattern

###值绑定模式语法

值绑定模式 → **var** 模式 | **let** 模式

###GRAMMAR OF A TUPLE PATTERN

‌ tuple-pattern → (tuple-pattern-element-list opt)

‌ tuple-pattern-element-list → tuple-pattern-element  tuple-pattern-element,tuple-pattern-element-list

‌ tuple-pattern-element → pattern

###元组模式语法
元组模式 → ( 元组模式元素列表 可选 )

元组模式元素列表 → 元组模式元素 | 元组模式元素 , 元组模式元素列表

元组模式元素 → 模式

###GRAMMAR OF AN ENUMERATION CASE PATTERN

‌ enum-case-pattern → type-identifier opt.enum-case-nametuple-pattern opt

###枚举用例模式语法

枚举用例模式 → 类型标识 可选 . 枚举的case名 元组模式 可选


###GRAMMAR OF A TYPE CASTING PATTERN

‌ type-casting-pattern → is-pattern  as-pattern

‌ is-pattern → istype

‌ as-pattern → patternastype
###类型转换模式语法
类型转换模式 → is模式 | as模式

is模式 → **is** 类型

as模式 → 模式 **as** 类型

###GRAMMAR OF AN EXPRESSION PATTERN

‌ expression-pattern → expression

###表达式模式语法
表达式模式 → 表达式

##Attributes
##属性

###GRAMMAR OF AN ATTRIBUTE

‌ attribute → @ attribute-nameattribute-argument-clause opt

‌ attribute-name → identifier

‌ attribute-argument-clause → (balanced-tokens opt)

‌ attributes → attribute attributes opt

‌ balanced-tokens → balanced-token balanced-tokens opt

‌ balanced-token → (balanced-tokens opt)

‌ balanced-token → [balanced-tokens opt]

‌ balanced-token → {balanced-tokens opt}

‌ balanced-token → Any identifier, keyword, literal, or operator

‌ balanced-token → Any punctuation except (, ), [, ], {, or }
####属性语法
属性 → @ 属性名 属性参数子句 可选

属性名 → 标识符

属性参数子句 → ( 平衡令牌列表 可选 )

属性列表 → 属性 属性列表 可选

平衡令牌列表 → 平衡令牌 平衡令牌列表 可选

平衡令牌 → **(** 平衡令牌列表 可选 **)**

平衡令牌 → **[** 平衡令牌列表 可选 **]**

平衡令牌 → **{** 平衡令牌列表 可选 **}**

平衡令牌 → 任意标识符, 关键字, 字面量或运算符

平衡令牌 → 任意标点除了**(, ), [, ], {,** 或 **}**

##Expressions
##表达式
###GRAMMAR OF AN EXPRESSION

‌ expression → prefix-expressionbinary-expressions opt

‌ expression-list → expression | expression , expression-list

###表达式语法
表达式 → 前置表达式 二元表达式列表 可选

表达式列表 → 表达式 | 表达式 **,** 表达式列表

GRAMMAR OF A PREFIX EXPRESSION

‌ prefix-expression → prefix-operator opt postfix-expression
‌ prefix-expression → in-out-expression
‌ in-out-expression → & identifier

###前置表达式语法
前置表达式 → 前置运算符 可选 后置表达式

前置表达式 → 写入写出表达式

写入写出表达式 → **&** 标识符

###GRAMMAR OF A BINARY EXPRESSION

‌ binary-expression → binary-operator prefix-expression

‌ binary-expression → assignment-operator prefix-expression

‌ binary-expression → conditional-operator prefix-expression

‌ binary-expression → type-casting-operator

‌ binary-expressions → binary-expression binary-expressionsopt

###二元表达式语法
二元表达式 → 二元运算符 前置表达式

二元表达式 → 赋值运算符 前置表达式

二元表达式 → 条件运算符 前置表达式

二元表达式 → 类型转换运算符

二元表达式列表 → 二元表达式 二元表达式列表 可选

###GRAMMAR OF AN ASSIGNMENT OPERATOR

‌ assignment-operator → =
###赋值运算符语法
赋值运算符 → **=**

###GRAMMAR OF A CONDITIONAL OPERATOR

‌ conditional-operator → ? expression :

###三元条件运算符语法
三元条件运算符 → **?** 表达式 **:**

###GRAMMAR OF A TYPE-CASTING OPERATOR

‌ type-casting-operator → is type | as ? opttype

###类型转换运算符语法
类型转换运算符 → **is** 类型 | **as ?** 可选 类型

###GRAMMAR OF A PRIMARY EXPRESSION

‌ primary-expression → identifiergeneric-argument-clause opt

‌ primary-expression → literal-expression

‌ primary-expression → self-expression

‌ primary-expression → superclass-expression

‌ primary-expression → closure-expression

‌ primary-expression → parenthesized-expression

‌ primary-expression → implicit-member-expression

‌ primary-expression → wildcard-expression


###主表达式语法
主表达式 → 标识符 泛型参数子句 可选

主表达式 → 字面量表达式

主表达式 → self表达式

主表达式 → 超类表达式

主表达式 → 闭包表达式

主表达式 → 圆括号表达式

主表达式 → 隐式成员表达式

主表达式 → 通配符表达式

###GRAMMAR OF A LITERAL EXPRESSION

‌ literal-expression → literal

‌ literal-expression → array-literal | dictionary-literal

‌ literal-expression → __FILE__ | __LINE__ | __COLUMN__ | __FUNCTION__

‌ array-literal → [array-literal-items opt]

‌ array-literal-items → array-literal-item,opt  array-literal-item,array-literal-items

‌ array-literal-item → expression

‌ dictionary-literal → [dictionary-literal-items]  [:]

‌ dictionary-literal-items → dictionary-literal-item,opt dictionary-literal-item,dictionary-literal-items

‌ dictionary-literal-item → expression:expression
###字面量表达式语法
字面量表达式 → 字面量

字面量表达式 → 数组字面量 | 字典字面量

字面量表达式 → __FILE__ | __LINE__ | __COLUMN__ | __FUNCTION__

数组字面量 → [ 数组字面量项列表 可选 ]

数组字面量项列表 → 数组字面量项 , 可选 | 数组字面量项 , 数组字面量项列表

数组字面量项 → 表达式

字典字面量 → [ 字典字面量项列表 ] | [ : ]

字典字面量项列表 → 字典字面量项 , 可选 | 字典字面量项 , 字典字面量项列表

字典字面量项 → 表达式 : 表达式

###GRAMMAR OF A SELF EXPRESSION

‌ self-expression → self

‌ self-expression → self.identifier

‌ self-expression → self[expression]

‌ self-expression → self.init

###Self 表达式语法
self表达式 → **self**

self表达式 → **self** **.** 标识符

self表达式 → **self** [ 表达式 ]

self表达式 → **self . init**

###GRAMMAR OF A SUPERCLASS EXPRESSION

‌ superclass-expression → superclass-method-expression | superclass-subscript-expression  |superclass-initializer-expression
‌ 
superclass-method-expression → super.identifier
‌ 
superclass-subscript-expression → super[expression]
‌ 
superclass-initializer-expression → super.init
###超类表达式语法
超类表达式 → 超类方法表达式 | 超类下标表达式 | 超类构造器表达式

超类方法表达式 → **super . **标识符

超类下标表达式 → **super [** 表达式 **]**

超类构造器表达式 → **super . init**

###GRAMMAR OF A CLOSURE EXPRESSION

‌ closure-expression → {closure-signature opt statements}

‌ closure-signature → parameter-clause function-result opt in

‌ closure-signature → identifier-list function-result opt in

‌ closure-signature → capture-listp arameter-clause function-result opt in

‌ closure-signature → capture-list identifier-list function-result opt in

‌ closure-signature → capture-list in

‌ capture-list → [capture-specifierexpression]

‌ capture-specifier → weak  unowned  unowned(safe) unowned(unsafe)

###闭包表达式语法

闭包表达式 → **{** 闭包签名 可选 多条语句 **}**

闭包签名 → 参数子句 函数结果 可选 **in**

闭包签名 → 标识符列表 函数结果 可选 **in**

闭包签名 → 捕获列表 参数子句 函数结果 可选 **in**

闭包签名 → 捕获列表 标识符列表 函数结果 可选 **in**

闭包签名 → 捕获列表 **in**

捕获列表 → **[** 捕获说明符 表达式 **]**

捕获说明符 → **weak** |**unowned** | **unowned(safe)** | **unowned(unsafe)**

###GRAMMAR OF A IMPLICIT MEMBER EXPRESSION

‌ implicit-member-expression → .identifier
###隐式成员表达式语法
隐式成员表达式 → **.** 标识符

###GRAMMAR OF A PARENTHESIZED EXPRESSION

‌ parenthesized-expression → (expression-element-list opt)

‌ expression-element-list → expression-element | expression-element,expression-element-list

‌ expression-element → expression | identifier:expression

###圆括号表达式语法

圆括号表达式 → **(**表达式元素列表 可选 **)**

表达式元素列表 → 表达式元素 | 表达式元素 , 表达式元素列表

表达式元素 → 表达式 | 标识符 **:** 表达式

###GRAMMAR OF A WILDCARD EXPRESSION

‌ wildcard-expression → _
###通配符表达式语法
通配符表达式 → _

###GRAMMAR OF A POSTFIX EXPRESSION

‌ postfix-expression → primary-expression

‌ postfix-expression → postfix-expressionpostfix-operator

‌ postfix-expression → function-call-expression

‌ postfix-expression → initializer-expression

‌ postfix-expression → explicit-member-expression

‌ postfix-expression → postfix-self-expression

‌ postfix-expression → dynamic-type-expression

‌ postfix-expression → subscript-expression

‌ postfix-expression → forced-value-expression

‌ postfix-expression → optional-chaining-expression

###后置表达式语法

后置表达式 → 主表达式

后置表达式 → 后置表达式 后置运算符

后置表达式 → 函数调用表达式

后置表达式 → 构造器表达式

后置表达式 → 显示成员表达式

后置表达式 → 后置self表达式

后置表达式 → 动态类型表达式

后置表达式 → 下标表达式

后置表达式 → 强制取值表达式

后置表达式 → 可选表达式

###GRAMMAR OF A FUNCTION CALL EXPRESSION

‌ function-call-expression → postfix-expressionparenthesized-expression

‌ function-call-expression → postfix-expressionparenthesized-expressionopttrailing-closure

‌ trailing-closure → closure-expression
###函数调用表达式语法
函数调用表达式 → 后置表达式 圆括号表达式

函数调用表达式 → 后置表达式 圆括号表达式 可选 后置闭包

后置闭包 → 闭包表达式

###GRAMMAR OF AN INITIALIZER EXPRESSION

‌ initializer-expression → postfix-expression .init
###构造器表达式语法
构造器表达式 → 后置表达式 **. init**

###GRAMMAR OF AN EXPLICIT MEMBER EXPRESSION

‌ explicit-member-expression → postfix-expression . decimal-digit

‌ explicit-member-expression → postfix-expression . identifier generic-argument-clause opt

###显式成员表达式语法
显示成员表达式 → 后置表达式 . 十进制数字

显示成员表达式 → 后置表达式 . 标识符 泛型参数子句 可选

###GRAMMAR OF A SELF EXPRESSION

‌ postfix-self-expression → postfix-expression .self

###后置Self 表达式语法
后置self表达式 → 后置表达式 **. self**

###GRAMMAR OF A DYNAMIC TYPE EXPRESSION

‌ dynamic-type-expression → postfix-expression . dynamicType

###动态类型表达式语法

动态类型表达式 → 后置表达式 **. dynamicType**

###GRAMMAR OF A SUBSCRIPT EXPRESSION

‌ subscript-expression → postfix-expression [ expression-list ]

###附属脚本表达式语法
附属脚本表达式 → 后置表达式 **[** 表达式列表 **]**

###GRAMMAR OF A FORCED-VALUE EXPRESSION

‌ forced-value-expression → postfix-expression !
###强制取值语法

强制取值表达式 → 后置表达式 **!**

###GRAMMAR OF AN OPTIONAL-CHAINING EXPRESSION

‌ optional-chaining-expression → postfix-expression ?
##可选表达式语法
可选表达式 → 后置表达式 **?**

##Lexical Structure
##词法结构

###GRAMMAR OF AN IDENTIFIER

‌ identifier → identifier-head identifier-characters opt

‌ identifier → ` identifier-head identifier-characters opt `

‌ identifier → implicit-parameter-name

‌ identifier-list → identifier | identifier,identifier-list

‌ identifier-head → Upper- or lowercase letter A through Z

‌ identifier-head → U+00A8, U+00AA, U+00AD, U+00AF, U+00B2–U+00B5, or U+00B7–U+00BA

‌ identifier-head → U+00BC–U+00BE, U+00C0–U+00D6, U+00D8–U+00F6, or U+00F8–U+00FF

‌ identifier-head → U+0100–U+02FF, U+0370–U+167F,U+1681–U+180D, or U+180F–U+1DBF

‌ identifier-head → U+1E00–U+1FFF

‌ identifier-head → U+200B–U+200D, U+202A–U+202E, U+203F–U+2040, U+2054, or U+2060–U+206F

‌ identifier-head → U+2070–U+20CF, U+2100–U+218F, U+2460–U+24FF, or U+2776–U+2793

‌ identifier-head → U+2C00–U+2DFF or U+2E80–U+2FFF

‌ identifier-head → U+3004–U+3007, U+3021–U+302F, U+3031–U+303F, or U+3040–U+D7FF

‌ identifier-head → U+F900–U+FD3D, U+FD40–U+FDCF, U+FDF0–U+FE1F, or U+FE30–U+FE44

‌ identifier-head → U+FE47–U+FFFD

‌ identifier-head → U+10000–U+1FFFD, U+20000–U+2FFFD, U+30000–U+3FFFD, or U+40000–U+4FFFD

‌ identifier-head → U+50000–U+5FFFD, U+60000–U+6FFFD, U+70000–U+7FFFD, or U+80000–U+8FFFD

‌ identifier-head → U+90000–U+9FFFD, U+A0000–U+AFFFD, U+B0000–U+BFFFD, or U+C0000–U+CFFFD

‌ identifier-head → U+D0000–U+DFFFD or U+E0000–U+EFFFD

‌ identifier-character → Digit 0 through 9

‌ identifier-character → U+0300–U+036F, U+1DC0–U+1DFF, U+20D0–U+20FF, or U+FE20–U+FE2F

‌ identifier-character → identifier-head

‌ identifier-characters → identifier-characteridentifier-characters opt

‌ implicit-parameter-name → $ decimal-digits

###标识符语法

标识符 → 标识符头 标识符字符列表 可选

标识符 → ` 标识符头 标识符字符列表 可选 `

标识符 → 隐式参数名

标识符列表 → 标识符 | 标识符 , 标识符列表

标识符头 → 大写或者 小写的字母 A 到 Z

标识符头 → U+00A8, U+00AA, U+00AD, U+00AF, U+00B2–U+00B5, 或者 U+00B7–U+00BA

标识符头 → U+00BC–U+00BE, U+00C0–U+00D6, U+00D8–U+00F6, 或者 U+00F8–U+00FF

标识符头 → U+0100–U+02FF, U+0370–U+167F, U+1681–U+180D, 或者 U+180F–U+1DBF

标识符头 → U+1E00–U+1FFF

标识符头 → U+200B–U+200D, U+202A–U+202E, U+203F–U+2040, U+2054, 或者 U+2060–U+206F

标识符头 → U+2070–U+20CF, U+2100–U+218F, U+2460–U+24FF, 或者 U+2776–U+2793

标识符头 → U+2C00–U+2DFF 或者 U+2E80–U+2FFF

标识符头 → U+3004–U+3007, U+3021–U+302F, U+3031–U+303F, 或者 U+3040–U+D7FF

标识符头 → U+F900–U+FD3D, U+FD40–U+FDCF, U+FDF0–U+FE1F, 或者 U+FE30–U+FE44

标识符头 → U+FE47–U+FFFD

标识符头 → U+10000–U+1FFFD, U+20000–U+2FFFD, U+30000–U+3FFFD, 或者 U+40000–U+4FFFD

标识符头 → U+50000–U+5FFFD, U+60000–U+6FFFD, U+70000–U+7FFFD, 或者 U+80000–U+8FFFD

标识符头 → U+90000–U+9FFFD, U+A0000–U+AFFFD, U+B0000–U+BFFFD, 或者 U+C0000–U+CFFFD

标识符头 → U+D0000–U+DFFFD 或者 U+E0000–U+EFFFD

标识符字符 → 数字 0 到 9

标识符字符 → U+0300–U+036F, U+1DC0–U+1DFF, U+20D0–U+20FF, 或者 U+FE20–U+FE2F

标识符字符 → 标识符头

标识符字符列表 → 标识符字符 标识符字符列表 可选

隐式参数名 → **$** 十进制数字列表


###GRAMMAR OF A LITERAL

‌ literal → integer-literal | floating-point-literal | string-literal

###字面量语法
字面量 → 整型字面量 | 浮点数字面量 | 字符串字面量


###GRAMMAR OF AN INTEGER LITERAL

‌ integer-literal → binary-literal

‌ integer-literal → octal-literal

‌ integer-literal → decimal-literal

‌ integer-literal → hexadecimal-literal

‌ binary-literal → 0b binary-digitbinary-literal-characters opt

‌ binary-digit → Digit 0 or 1

‌ binary-literal-character → binary-digit  _

‌ binary-literal-characters → binary-literal-characterbinary-literal-characters opt

‌ octal-literal → 0ooctal-digitoctal-literal-characters opt

‌ octal-digit → Digit 0 through 7

‌ octal-literal-character → octal-digit  _

‌ octal-literal-characters → octal-literal-characteroctal-literal-characters opt

‌ decimal-literal → decimal-digitdecimal-literal-characters opt

‌ decimal-digit → Digit 0 through 9

‌ decimal-digits → decimal-digitdecimal-digits opt

‌ decimal-literal-character → decimal-digit  _

‌ decimal-literal-characters → decimal-literal-characterdecimal-literal-characters opt

‌ hexadecimal-literal → 0xhexadecimal-digithexadecimal-literal-characters opt

‌ hexadecimal-digit → Digit 0 through 9, a through f, or A through F

‌ hexadecimal-literal-character → hexadecimal-digit  _

‌ hexadecimal-literal-characters → hexadecimal-literal-characterhexadecimal-literal-characters opt
###整型字面量语法
整型字面量 → 二进制字面量

整型字面量 → 八进制字面量

整型字面量 → 十进制字面量

整型字面量 → 十六进制字面量

二进制字面量 → **0b** 二进制数字 二进制字面量字符列表 可选

二进制数字 → 数字 0 到 1

二进制字面量字符 → 二进制数字 | _

二进制字面量字符列表 → 二进制字面量字符 二进制字面量字符列表 可选

八进制字面量 →** 0o** 八进字数字 八进制字符列表 可选

八进字数字 → 数字 0 到 7

八进制字符 → 八进字数字 | _

八进制字符列表 → 八进制字符 八进制字符列表 可选

十进制字面量 → 十进制数字 十进制字符列表 可选

十进制数字 → 数字 0 到 9

十进制数字列表 → 十进制数字 十进制数字列表 可选

十进制字符 → 十进制数字 | _

十进制字符列表 → 十进制字符 十进制字符列表 可选

十六进制字面量 → **0x **十六进制数字 十六进制字面量字符列表 可选

十六进制数字 → 数字 0 到 9, a 到 f, or A 到 F

十六进制字符 → 十六进制数字 | _

十六进制字面量字符列表 → 十六进制字符 十六进制字面量字符列表 可选

###GRAMMAR OF A FLOATING-POINT LITERAL

‌ floating-point-literal → decimal-literal decimal-fraction opt decimal-exponentopt

‌ floating-point-literal → hexadecimal-literal hexadecimal-fraction opt hexadecimal-exponent

‌ decimal-fraction → .decimal-literal

‌ decimal-exponent → floating-point-esign opt decimal-literal

‌ hexadecimal-fraction → .hexadecimal-literal opt

‌ hexadecimal-exponent → floating-point-psign opt hexadecimal-literal

‌ floating-point-e → e | E

‌ floating-point-p → p | P

‌ sign → + | -

###浮点型字面量语法
浮点数字面量 → 十进制字面量 十进制分数 可选 十进制指数 可选

浮点数字面量 → 十六进制字面量 十六进制分数 可选 十六进制指数

十进制分数 → . 十进制字面量

十进制指数 → 浮点数e 正负号 可选 十进制字面量

十六进制分数 → . 十六进制字面量 可选

十六进制指数 → 浮点数p 正负号 可选 十六进制字面量

浮点数e → **e** | **E**

浮点数p → **p** | **P**

正负号 → **+** |** -**

###GRAMMAR OF A STRING LITERAL

‌ string-literal → "quoted-text"

‌ quoted-text → quoted-text-item quoted-text opt

‌ quoted-text-item → escaped-character

‌ quoted-text-item → \(expression)

‌ quoted-text-item → Any Unicode extended grapheme cluster except ", \, U+000A, or U+000D

‌ escaped-character → \0  \\  \t  \n  \r  \" \'

‌ escaped-character → \x hexadecimal-digit hexadecimal-digit

‌ escaped-character → \u hexadecimal-digit hexadecimal-digit hexadecimal-digit hexadecimal-digit

‌ escaped-character → \U hexadecimal-digit hexadecimal-digit hexadecimal-digit hexadecimal-digit hexadecimal-digit hexadecimal-digit hexadecimal-digit hexadecimal-digit

###字符型字面量语法
字符串字面量 → **"** 引用文本** "**

引用文本 → 引用文本条目 引用文本 可选

引用文本条目 → 转义字符

引用文本条目 → **\(** 表达式 **)**

引用文本条目 → 除了"­, \­, U+000A, 或者 U+000D外的所有Unicode的字符

转义字符 → **\0**| **\\** | **\t** | **\n** | **\r** | **\"** | **\'**

转义字符 → **\x** 十六进制数字 十六进制数字

转义字符 → **\u** 十六进制数字 十六进制数字 十六进制数字 十六进制数字

转义字符 → **\U** 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字 十六进制数字

###GRAMMAR OF OPERATORS

‌ operator → operator-character operator opt

‌ operator-character → /  =  -  +  !  *  %  <  >  &  |  ^  ~  .


‌ binary-operator → operator

‌ prefix-operator → operator

‌ postfix-operator → operator

###运算符语法语法

运算符 → 运算符字符 运算符 可选

运算符字符 → **/** | **=** | **-** | **+** | **!** | ***** | **%** | **<** | **>** | **&** | **|** | **^** | **~** | **.**

二元运算符 → 运算符

前置运算符 → 运算符

后置运算符 → 运算符

##Types
##类型

###GRAMMAR OF A TYPE

‌ type → array-type | function-type | type-identifier | tuple-type | optional-type | implicitly-unwrapped-optional-type | protocol-composition-type | metatype-type

###类型语法
类型 → 数组类型 | 函数类型 | 类型标识 | 元组类型 | 可选类型 | 隐式解析可选类型 | 协议合成类型 | 元型类型


###GRAMMAR OF A TYPE ANNOTATION

‌ type-annotation → :attributes opt type
###类型注解语法

类型注解 → : 属性列表 可选 类型

###GRAMMAR OF A TYPE IDENTIFIER

‌ type-identifier → type-name generic-argument-clause opt type-name generic-argument-clauseopt.type-identifier

‌ type-name → identifier
###类型标识语法
类型标识 → 类型名称 泛型参数子句 可选 | 类型名称 泛型参数子句 可选 . 类型标识

类名 → 标识符

###GRAMMAR OF A TUPLE TYPE

‌ tuple-type → (tuple-type-body opt)

‌ tuple-type-body → tuple-type-element-list...opt

‌ tuple-type-element-list → tuple-type-element |  tuple-type-element,tuple-type-element-list

‌ tuple-type-element → attributes opt inout opt type inout opt element-nametype-annotation

‌ element-name → identifier

###元组类型语法
元组类型 → ( 元组类型主体 可选 )

元组类型主体 → 元组类型的元素列表 ... 可选

元组类型的元素列表 → 元组类型的元素 | 元组类型的元素 , 元组类型的元素列表

元组类型的元素 → 属性列表 可选 **inout** 可选 类型 | **inout** 可选 元素名 类型注解

元素名 → 标识符

###GRAMMAR OF A FUNCTION TYPE

‌ function-type → type->type

###函数类型语法
函数类型 → 类型 → 类型

###GRAMMAR OF AN ARRAY TYPE

‌ array-type → type | array-type
###数组类型语法
数组类型 → 类型** [ ]**  数组类型 **[ ]**

###GRAMMAR OF AN OPTIONAL TYPE

‌ optional-type → type ?

###可选类型语法
可选类型 → 类型 **?**

###GRAMMAR OF AN IMPLICITLY UNWRAPPED OPTIONAL TYPE

‌ implicitly-unwrapped-optional-type → type !

###隐式解析可选类型语法

隐式解析可选类型 → 类型 !

###GRAMMAR OF A PROTOCOL COMPOSITION TYPE

‌ protocol-composition-type → protocol <protocol-identifier-list opt>

‌ protocol-identifier-list → protocol-identifier  protocol-identifier,protocol-identifier-list
 
‌ protocol-identifier → type-identifier

###协议合成类型语法
协议合成类型 → **protocol** < 协议标识符列表 可选 >

协议标识符列表 → 协议标识符 | 协议标识符 , 协议标识符列表

协议标识符 → 类型标识

###GRAMMAR OF A METATYPE TYPE

‌ metatype-type → type.Type  type.Protocol
###元类型语法
元类型 → 类型 **.** **Type** | 类型 **.** **Protocol**

###GRAMMAR OF A TYPE INHERITANCE CLAUSE

‌ type-inheritance-clause → :type-inheritance-list

‌ type-inheritance-list → type-identifier | type-identifier,type-inheritance-list

###类型继承子句语法
类型继承子句 → : 类型继承列表

类型继承列表 → 类型标识 | 类型标识 , 类型继承列表

