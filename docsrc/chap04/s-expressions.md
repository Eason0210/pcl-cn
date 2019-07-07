# S-expressions（S-表达式）

The basic elements of s-expressions are lists and atoms. Lists are
delimited by parentheses and can contain any number of
whitespace-separated elements. Atoms are everything else.5 The
elements of lists are themselves s-expressions (in other words, atoms
or nested lists). Comments--which aren't, technically speaking,
s-expressions--start with a semicolon, extend to the end of a line,
and are treated essentially like whitespace.

S-表达式的基本元素是列表（list）和原子（atom）。列表由括号所包围，并可包含任何数量的由空格所分隔的元素。原子是所有其他内容。列表元素本身也可以是
S-表达式（换句话说，也就是原子或嵌套的列表）。注释——从技术角度来讲不是
S-表达式，它们以分号开始，直到一行的结尾，本质上将被当作空白来处理。

And that's pretty much it. Since lists are syntactically so trivial,
the only remaining syntactic rules you need to know are those
governing the form of different kinds of atoms. In this section I'll
describe the rules for the most commonly used kinds of atoms: numbers,
strings, and names. After that, I'll cover how s-expressions composed
of these elements can be evaluated as Lisp forms.

这就差不多了。列表在句法上十分简单，你需要知道的句法规则只有那些用来形成不同类型原子的规则了。在本节里我将描述几种常用原子类型的规则，这些原子包括：数字、字符串和名字。之后我将说明由这些元素所组成的
S-表达式是如何被作为 Lisp 形式求值的。

Numbers are fairly straightforward: any sequence of digits--possibly
prefaced with a sign (+ or -), containing a decimal point (.) or a
solidus (/), or ending with an exponent marker--is read as a
number. For example:

数字的表示方法相当直接：任何数位的序列——可能有一个前缀标识（`+` 或 `-`），还可能会有一个十进制点（`.`）或者斜杠（`/`），或是以一个指数标记结尾——将被读取为一个数字。例如：

```lisp
123       ; the integer one hundred twenty-three（整数一百二十三）
3/7       ; the ratio three-sevenths（比值七分之三）
1.0       ; the floating-point number one in default precision（默认精度的浮点数 1）
1.0e0     ; another way to write the same floating-point number（同一个浮点数的另一种写法）
1.0d0     ; the floating-point number one in "double" precision（双精度的浮点数 1）
1.0e-4    ; the floating-point equivalent to one-ten-thousandth（等价于万分之一的浮点数）
+42       ; the integer forty-two（整数四十二）
-42       ; the integer negative forty-two（整数负四十二）
-1/4      ; the ratio negative one-quarter（比值负四分之一）
-2/8      ; another way to write negative one-quarter（负四分之一的另一种写法）
246/2     ; another way to write the integer one hundred twenty-three（整数一百二十三的另一种写法）
```

These different forms represent different kinds of numbers: integers,
ratios, and floating point. Lisp also supports complex numbers, which
have their own notation and which I'll discuss in Chapter 10.

这些不同的形式代表着不同类型的数字：整数、比值和浮点数。Lisp
也支持复数，但它们有其自己的表示法，第 10 章将予以介绍。

As some of these examples suggest, you can notate the same number in
many ways. But regardless of how you write them, all
rationals--integers and ratios--are represented internally in
"simplified" form. In other words, the objects that represent -2/8 or
246/2 aren't distinct from the objects that represent -1/4
and 123. Similarly, 1.0 and 1.0e0 are just different ways of writing
the same number. On the other hand, 1.0, 1.0d0, and 1 can all denote
different objects because the different floating-point representations
and integers are different types. We'll save the details about the
characteristics of different kinds of numbers for Chapter 10.

从这些示例可见，你可以用多种方式来表示同一个数字。但无论怎样书写，所有的有理数（整数和比值）在内部都被表示成
“简化” 形式。换句话说，表示 -2/8 或 246/2 的对象跟代表
-1/4 或 123 的对象并没有什么不同。与此相似，1.0 和 1.0e0
也只是同一个数字的不同写法而已。但另一方面，1.0、1.0d0 和 1
则可能会代表不同的对象，因为不同精度的浮点数和整数都是不同类型的对象。我将在第 10
章详细讨论不同类型数字的特征。

Strings literals, as you saw in the previous chapter, are enclosed in
double quotes. Within a string a backslash (\) escapes the next
character, causing it to be included in the string regardless of what
it is. The only two characters that must be escaped within a string
are double quotes and the backslash itself. All other characters can
be included in a string literal without escaping, regardless of their
meaning outside a string. Some example string literals are as follows:

正如在前面章节所看到的那样，字符串是由双引号所包围着的。在字符串中，一个反斜杠会转义接下来的任意字符，使其被包含在字符串里。两个在字符串中必须被转义的字符是双引号和反斜杠本身。所有其他的字符无需转义即可被包含在一个字符串，里无论它们在字符串之外有何含义。下面是一些字符串的示例：

```lisp
"foo"     ; the string containing the characters f, o, and o.（含有 f、o、和 o 的字符串）
"fo\o"    ; the same string（同一个字符串）
"fo\\o"   ; the string containing the characters f, o, \, and o.（含有 f、o、\、和 o 的字符串）
"fo\"o"   ; the string containing the characters f, o, ", and o.（含有 f、o、"、和 o 的字符串）
```

Names used in Lisp programs, such as **FORMAT** and `hello-world`, and `*db*`
are represented by objects called symbols. The reader knows nothing
about how a given name is going to be used--whether it's the name of a
variable, a function, or something else. It just reads a sequence of
characters and builds an object to represent the name.6 Almost any
character can appear in a name. Whitespace characters can't, though,
because the elements of lists are separated by whitespace. Digits can
appear in names as long as the name as a whole can't be interpreted as
a number. Similarly, names can contain periods, but the reader can't
read a name that consists only of periods. Ten characters that serve
other syntactic purposes can't appear in names: open and close
parentheses, double and single quotes, backtick, comma, colon,
semicolon, backslash, and vertical bar. And even those characters can,
if you're willing to escape them by preceding the character to be
escaped with a backslash or by surrounding the part of the name
containing characters that need escaping with vertical bars.

Lisp 程序中所使用的名字，诸如 **FORMAT**、`hello-world` 和 `*db*`
均由称为符号的对象所表示。读取器对于一个指定名字的用途毫不知情——无论其究竟用作变量、函数名还是其他什么东西。读取器只是读取字符序列并构造出此名所代表的对象。 几乎任何字符都可以出现在一个名字里，不过空白字符不可以，因为列表的元素是用空格来分隔的。数位也可以出现在名字里，只要整个名字不被解释成一个数字。类似地，名字可以包含句点，但读取器无法读取一个只由句点组成的名字。有十个字符被用于其他句法目的而不能出现在名字里，它们是：开放和闭合的圆括号、双引号和单引号、反引号、逗号、冒号、分号、反斜杠以及竖线。而就算是这些字符，如果你愿意的话，它们也可以成为名字的一部分，只需将它们用反斜杠转义起来，或是将含有需要转义的字符名字用竖线包起来。

Two important characteristics of the way the reader translates names
to symbol objects have to do with how it treats the case of letters in
names and how it ensures that the same name is always read as the same
symbol. While reading names, the reader converts all unescaped
characters in a name to their uppercase equivalents. Thus, the reader
will read `foo`, `Foo`, and `FOO` as the same symbol: `FOO`. However, `\f\o\o`
and `|foo|` will both be read as `foo`, which is a different object than
the symbol `FOO`. This is why when you define a function at the REPL and
it prints the name of the function, it's been converted to
uppercase. Standard style, these days, is to write code in all
lowercase and let the reader change names to uppercase.

这种读取器将名字转化成符号对象的方式有两个重要特征，一个是它如何处理名字中的字母大小写，另一个是它如何确保相同的名字总被读取成相同的符号。当读取名字时，读取器将所有名字中未转义的字符都转化成它们等价的大写形式。这样，读取器将把
`foo`、`Foo` 和 `FOO` 都读成同一个符号 `FOO`。但 `\f\o\o` 和 `|foo|`
都会被读成 `foo`，这是和符号 `FOO` 不同的另一个对象。这就是为什么在 REPL
中定义一个函数时，它的名字会被打印成大写形式的原因。近年来，标准的编码风格是将代码全部写成小写形式，然后让读取器将名字转化成大写。

To ensure that the same textual name is always read as the same
symbol, the reader interns symbols--after it has read the name and
converted it to all uppercase, the reader looks in a table called a
package for an existing symbol with the same name. If it can't find
one, it creates a new symbol and adds it to the table. Otherwise, it
returns the symbol already in the table. Thus, anywhere the same name
appears in any s-expression, the same object will be used to represent
it.

为了确保同一个文本名字总是被读取成相同的符号，读取器保留这个符号——在已取名字并将其全部转化成大写形式以后，读取器在一个称为包（package）的表里查询带有相同名字的已有符号。如果它无法找到，则将创建一个新符号并添加到表里。否则就将返回已在表中的那个符号。这样，无论在任何地方，同样的名字出现在任何
S-表达式里，都会用同一个对象去表示它。

Because names can contain many more characters in Lisp than they can
in Algol-derived languages, certain naming conventions are distinct to
Lisp, such as the use of hyphenated names like hello-world. Another
important convention is that global variables are given names that
start and end with `*`. Similarly, constants are given names starting
and ending in +. And some programmers will name particularly low-level
functions with names that start with `%` or even `%%`. The names defined
in the language standard use only the alphabetic characters (`A-Z`) plus
`*`, `+`, `-`, `/`, `1`, `2`, `<`, `=`, `>`, and `&`.

因为在 Lisp 中名字可以包含比源自 Algol 的语言更多的字符，故而命名约定在
Lisp 中也相应地有所不同，诸如可以使用像 `hello-world`
这类带有连字符的名字。另一个重要约定是全局变量名字在开始和结尾处带有
`*`。类似地，常量名都以 `+`
开始和结尾。而某些程序员则将特别底层的函数名前加 `%` 甚至
`%%`。语言标准所定义的名字只使用字母表字符（`A-Z`）外加
`*`、`+`、`-`、`/`、`1`、`2`、`<`、`=`、`>` 以及 `&`。

The syntax for lists, numbers, strings, and symbols can describe a
good percentage of Lisp programs. Other rules describe notations for
literal vectors, individual characters, and arrays, which I'll cover
when I talk about the associated data types in Chapters 10 and 11. For
now the key thing to understand is how you can combine numbers,
strings, and symbols with parentheses-delimited lists to build
s-expressions representing arbitrary trees of objects. Some simple
examples look like this:

只用列表、数字、字符串和符号就可以描述很大一部分的 Lisp
程序了。其他规则描述了字面向量、单个字符和数组的标识，我将在第 10
章和第 11
章里谈及相关的数据类型时再讲解它们。目前的关键是要理解怎样用数字、字符串和由符号借助括号所组成的列表来构建
S-表达式，从而表示任意的树状对象。下面是一些简单的例子。

```lisp
x             ; the symbol X（符号 X）
()            ; the empty list（空列表）
(1 2 3)       ; a list of three numbers（三个数字所组成的列表）
("foo" "bar") ; a list of two strings（两个字符串所组成的列表）
(x y z)       ; a list of three symbols（三个符号所组成的列表）
(x 1 "foo")   ; a list of a symbol, a number, and a string（由一个符号、一个数字和一个字符串所组成的列表）
(+ (* 2 3) 4) ; a list of a symbol, a list, and a number.（由一个符号、一个列表和一个数字所组成的列表）
```

An only slightly more complex example is the following four-item list
that contains two symbols, the empty list, and another list, itself
containing two symbols and a string:

下面这种四元素列表就生活稍显复杂了，它含有两个符号、空列表以及另一个列表——其本身又含有两个符号和两个字符串：

```lisp
(defun hello-world ()
  (format t "hello, world"))
```
