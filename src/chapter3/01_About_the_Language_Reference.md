# Language Reference

## About the Language Reference
## 关于语言参考

This part of the book describes the formal grammar of the Swift programming language.The grammar described here is intended to help you understand the language in more detail, rather than to allow you to directly implement a parser or compiler.


本书的该部分描述了Swift编程语言的正式语法。在此描述语法的目的是为了帮助你更详细的理解该语言，而不是让你直接实现一个解析器或编译器。

The Swift language is relatively small, because many common types, functions, and operators that appear virtually everywhere in Swift code are actually defined in the Swift standard library. Although these types, functions, and operators are not part of the Swift language itself, they are used extensively in the discussions and code examples in this
part of the book.

Swift语言相对较小，因为那些无处不在出现在Swift代码中的很多常见的类型，函数，和运算符实际上已经定义在了Swift的标准库中。虽然这些类型，函数，和运算符本身不是Swift语言的一部分，但它们被广泛应用于该书本部分的探讨和代码示例中。

## How to Read the Grammar
## 如何阅读语法
The notation used to describe the formal grammar of the Swift programming language follows a few conventions:

用于描述Swift编程语言正规语法的标记有如下几个约定：

 * An arrow (→) is used to mark grammar productions and can be read as “can consist of.“

* 箭头(→)用于标记语法生产和可以理解为“可包括”

* Syntactic categories are indicated by italic text and appear on both sides of a grammar production rule.

* 语法范围以斜体文字表示，显示在语法规范的两侧。

* Literal words and punctuation are indicated by boldface constant width text and appear only on the right-hand side of a grammar production rule.

* 文字和标点由固定宽度的粗体文字显示，并只出现在一个语法生产规范的右侧.
* Alternative grammar productions are separated by vertical bars (|). When alternative productions are too long to read easily, they are broken into multiple grammar production rules on new lines.

* 替代语法产生式由竖线(|)分隔。当替代产生式过长而不易阅读时，它们将在新行中变换为多个语法产生式规范。

* In a few cases, regular font text is used to describe the right-hand side of a grammar production rule.

* 在一些案例中，常规字体文本将用于描述右侧的语法产生式规则。

* Optional syntactic categories and literals are marked by a trailing subscript, opt.

* 可选的句法范围和文字为在尾部以opt标识描述。

As an example, the grammar of a getter-setter block is defined as follows:

比如，getter-setter 区的语法定义如下：

> G R A M M A R O F A G E T T E R- S E T T E R B L O C K

> getter-setter-block → { getter-clause setter-clause opt } ｜{ setter-clause getter clause
}

This definition indicates that a getter-setter block can consist of a getter clause followed by an optional setter clause, enclosed in braces, or a setter clause followed by a getter clause, enclosed in braces. The grammar production above is equivalent to the following two productions, where the alternatives are spelled out explicitly:

该定义表示，一个getter-setter方法块可由一个getter子句后跟一个可选的setter语句，括在大括号中。或者一个setter子句后跟一个getter子句，括在大括号中。上述语法产生式等价于下面的两个替代处已经明确拼写出的产生式。

> G R A M M A R O F A G E T T E R S E T T E R B L O C K

> getter-setter-block → { getter-clause setter-clause opt }

> getter-setter-block → { setter-clause getter-clause }


