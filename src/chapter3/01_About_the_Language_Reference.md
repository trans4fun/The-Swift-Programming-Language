# 语言参考

## 关于语言参考

本书的该部分描述了Swift编程语言的正式语法。在此描述语法的目的是为了帮助你更详细的理解该语言，而不是让你直接实现一个解析器或编译器。

Swift语言相对较小，因为那些无处不在出现在Swift代码中的很多常见的类型，函数，和运算符实际上已经定义在了Swift的标准库中。虽然这些类型，函数，和运算符不是Swift语言本身的一部分，但它们被广泛应用于该书本部分的探讨和代码示例中。

## 如何阅读语法

用于描述Swift编程语言正规语法的标记有如下几个约定：

* 箭头(→)用于标记文法和可以理解为“可包括”

* 语法范围以斜体文字表示，显示在语法规范的两侧。

* 文字和标点由固定宽度的粗体文字显示，并只出现在一个标记文法的右侧.

* 替代标记文法式由竖线(|)分隔。当替代文法过长而不易阅读时，它们将在新行中变换为多个标记文法规范。

* 在一些案例中，常规字体文本将用于描述右侧的标记文法规则。

* 可选的句法范围和字面量则以尾部下标opt作为标识。

比如，getter-setter 区的语法定义如下：

> GETTER-SETTER区语法

> getter-setter-block → { getter-clause setter-clause opt } ｜{ setter-clause getter clause}

该定义表示，一个getter-setter方法块可由一个getter子句后跟一个可选的setter语句，括在大括号中。或者一个setter子句后跟一个getter子句，括在大括号中。上述语法产生式等价于下面的两个替代处已经明确拼写出的产生式。

> GETTER-SETTER区语法

> getter-setter-block → { getter-clause setter-clause opt }

> getter-setter-block → { setter-clause getter-clause }


