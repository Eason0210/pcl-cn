# What's with All the Parentheses?（括号里都可以有什么）

Lisp's syntax is quite a bit different from the syntax of languages
descended from Algol. The two most immediately obvious characteristics
are the extensive use of parentheses and prefix notation. For whatever
reason, a lot of folks are put off by this syntax. Lisp's detractors
tend to describe the syntax as "weird" and "annoying." Lisp, they say,
must stand for Lots of Irritating Superfluous Parentheses. Lisp folks,
on the other hand, tend to consider Lisp's syntax one of its great
virtues. How is it that what's so off-putting to one group is a source
of delight to another?

Lisp 的语法和源自 Algol
的语言在语法上有很多不同。两者特征最明显的区别在于前者大量使用了括号和前缀表示法。说来也怪，大量的追随者都喜欢这样的语法。Lisp
的反对者们总是将这种语法描述成 “奇怪的” 和 “讨厌的”，他们说 Lisp
就是 “大量不合理的多余括号”（Lots of Irritating Superfluous
Parentheses）的简称；而 Lisp 的追随者则认为，Lisp
的语法是它的最大优势。为什么两个团体之间会有如此对立的见解呢？

I can't really make the complete case for Lisp's syntax until I've
explained Lisp's macros a bit more thoroughly, but I can start with an
historical tidbit that suggests it may be worth keeping an open mind:
when John McCarthy first invented Lisp, he intended to implement a
more Algol-like syntax, which he called M-expressions. However, he
never got around to it. He explained why not in his article "History
of Lisp."

在本章不可能完整地描述 Lisp 的语法，因为我还没有彻底地解释 Lisp
的宏，但我可以从一些宝贵的历史经验来说明保持开放的思想是值得的：John McCarthy
首次发明 Lisp 时，曾想过实现一种类 Algol 的语法，他称之为
M-表达式。尽管如此，他却从未实现这一点。他在自己的文章《History of Lisp》中对此加以解释。

> The project of defining M-expressions precisely and compiling them
> or at least translating them into S-expressions was neither
> finalized nor explicitly abandoned. It just receded into the
> indefinite future, and a new generation of programmers appeared who
> preferred [S-expressions] to any FORTRAN-like or ALGOL-like notation
> that could be devised.

> 这个精确定义 M-表达式以及将其编译或至少转译成
> S-表达式的工程，既没有完成也没有明确放弃，它只不过是被无限期地推迟了。（相比
> S-表达式）更加偏爱类 FORTRAN 或类 Algol 表示法的程序员新一代也许会最终实现它。

In other words, the people who have actually used Lisp over the past
45 years have liked the syntax and have found that it makes the
language more powerful. In the next few chapters, you'll begin to see
why.

换句话说，过去 45 年以来，实际使用 Lisp
的人们已经喜欢上了这种语法，并且发现它能使该语言变得更为强大。接下来的几章里将告诉你为什么会这样。
