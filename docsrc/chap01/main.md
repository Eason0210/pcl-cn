# Introduction: Why Lisp? 绪论：为什么是 Lisp？

If you think the greatest pleasure in programming comes from getting a
lot done with code that simply and clearly expresses your intention,
then programming in Common Lisp is likely to be about the most fun you
can have with a computer. You'll get more done, faster, using it than
you would using pretty much any other language.

如果你认为编程最大的乐趣在于可以用那些简单和清楚地表达你各种想法的代码来完成许多事，那么用
Common Lisp 编程可说是用计算机所能做到的最有趣的事了。相比很多其他的计算机语言，Common
Lisp 可以让你更快地完成更多工作。

That's a bold claim. Can I justify it? Not in a just a few pages in
this chapter--you're going to have to learn some Lisp and see for
yourself--thus the rest of this book. For now, let me start with some
anecdotal evidence, the story of my own road to Lisp. Then, in the
next section, I'll explain the payoff I think you'll get from learning
Common Lisp.

这是个大胆的断言。可我要怎样证明呢？当然不是用本章的只言片语了，而是这一整本书——你必须先学习一些
Lisp 知识才能体会到这一点。不过眼下，让我们先介绍一些轶事，即我本人迈向 Lisp
编程之路的经历。然后，在下一节里，我将说明你可以通过学习 Common Lisp 得到些什么收获。

I'm one of what must be a fairly small number of second-generation
Lisp hackers. My father got his start in computers writing an
operating system in assembly for the machine he used to gather data
for his doctoral dissertation in physics. After running computer
systems at various physics labs, by the 1980s he had left physics
altogether and was working at a large pharmaceutical company. That
company had a project under way to develop software to model
production processes in its chemical plants--if you increase the size
of this vessel, how does it affect annual production? The original
team, writing in FORTRAN, had burned through half the money and almost
all the time allotted to the project with nothing to show for their
efforts. This being the 1980s and the middle of the artificial
intelligence (AI) boom, Lisp was in the air. So my dad--at that point
not a Lisper--went to Carnegie Mellon University (CMU) to talk to some
of the folks working on what was to become Common Lisp about whether
Lisp might be a good language for this project.

我是极少数的所谓第二代 Lisp
黑客之一。我父亲的计算机生涯开始于用汇编语言给他的机器编写操作系统，从而为他的物理学博士论文搜集资料。在成功帮助了几家物理实验室用上计算机系统之后，从
20 世纪 80
年代起，他彻底抛弃了物理学，转而为一家大型制药公司工作。当时那家公司里有个软件项目，正在开发用于模拟化工生产过程的软件，比如说，增大容器的尺寸将会怎样影响其年产量。原先的团队使用
FORTRAN 进行开发，已经耗费了该项目的一半预算和几乎全部的时间，却还是没能交付任何成果。那是在
20 世纪 80 年代，人工智能（AI）蓬勃发展，Lisp
正在流行。于是，我父亲（当时还不是 Lisp 程序员）来到卡内基梅隆大学（CMU），向那些正在开发后来被称为
Common Lisp语言的人们咨询：如果用 Lisp 来开发这个项目是否合适？

The CMU folks showed him some demos of stuff they were working on, and
he was convinced. He in turn convinced his bosses to let his team take
over the failing project and do it in Lisp. A year later, and using
only what was left of the original budget, his team delivered a
working application with features that the original team had given up
any hope of delivering. My dad credits his team's success to their
decision to use Lisp.

CMU 的人向我父亲演示了一些他们正在做的东西，于是他被说服了。然后他又说服老板让他的团队接手那个失败的项目并用
Lisp 重新开发。一年以后，仅仅使用了原先剩余的预算，他的团队就交付了一个可用的应用程序，而且还带有已经被原先团队所放弃的一些功能。我父亲将其团队的成功原因归结为他们使用了 Lisp。

Now, that's just one anecdote. And maybe my dad is wrong about why
they succeeded. Or maybe Lisp was better only in comparison to other
languages of the day. These days we have lots of fancy new languages,
many of which have incorporated features from Lisp. Am I really saying
Lisp can offer you the same benefits today as it offered my dad in the
1980s? Read on.

当然，仅此一例还不足以说明问题，而且也有可能我父亲对其成功原因认识有误，或者也许 Lisp
仅仅在那个年代才可以跟其他语言相媲美。如今我们有了大量精巧的新语言，它们中的许多都吸收了
Lisp 的特性。是否真的可以说，Lisp 在现今也具有跟我父亲那个年代一样的优势吗？请继续往下读。

Despite my father's best efforts, I didn't learn any Lisp in high
school. After a college career that didn't involve much programming in
any language, I was seduced by the Web and back into computers. I
worked first in Perl, learning enough to be dangerous while building
an online discussion forum for Mother Jones magazine's Web site and
then moving to a Web shop, Organic Online, where I worked on big--for
the time--Web sites such as the one Nike put up during the 1996
Olympics. Later I moved onto Java as an early developer at WebLogic,
now part of BEA. After WebLogic, I joined another startup where I was
the lead programmer on a team building a transactional messaging
system in Java. Along the way, my general interest in programming
languages led me to explore such mainstream languages as C, C++, and
Python, as well as less well-known ones such as Smalltalk, Eiffel, and
Beta.

尽管父亲作了大量努力，但我直到高中也没有学过一点儿
Lisp。在大学时代我也没怎么用任何语言来写程序，是后来出现的
Web 让我回到了计算机的怀抱。我首先使用的是Perl，先是为 Mother
Jones 杂志的网站构建在线论坛，待经验丰富以后转向 Web 商店 Organic
Online，在那里我为当时的大型 Web 站点工作，例如耐克公司在
1996 年奥运会期间上线的站点。后来我转向 Java，并成为 WebLogic（现在是
BEA 的一部分）的早期开发者。离开 WebLogic
以后，我又作为另一个团队的首席程序员开始用 Java
编写事务消息系统。在此期间，对编程语言的广泛兴趣使我充分研究了诸如 C、
C++ 和 Python 这些主流语言，以及 Smalltalk、Eiffel 和 Beta
这些小众语言。

So I knew two languages inside and out and was familiar with another
half dozen. Eventually, however, I realized my interest in programming
languages was really rooted in the idea planted by my father's tales
of Lisp--that different languages really are different, and that,
despite the formal Turing equivalence of all programming languages,
you really can get more done more quickly in some languages than
others and have more fun doing it. Yet, ironically, I had never spent
that much time with Lisp itself. So, I started doing some Lisp hacking
in my free time. And whenever I did, it was exhilarating how quickly I
was able to go from idea to working code.

所以我对 Perl 和 Java
两种语言了如指掌，同时还熟悉其他不下六种语言。不过最终我还是意识到，我对编程语言的兴趣其实来源于记忆之中的我父亲的
Lisp 经历——语言之间真的有天壤之别，尽管所有的编程语言在形式上都是图灵等价的，但一些语言真的会比其他语言更快更好地完成某些事情，并且在使用的过程中还能给你带来更多的乐趣。不过可笑的是，我从没有在
Lisp 上花太多时间。于是我开始利用业余时间研究
Lisp。无论我做什么，最令我兴奋的始终是可以很快地将思路变成可用的代码。

For example, one vacation, having a week or so to hack Lisp, I decided
to try writing a version of a program--a system for breeding genetic
algorithms to play the game of Go--that I had written early in my
career as a Java programmer. Even handicapped by my then rudimentary
knowledge of Common Lisp and having to look up even basic functions,
it still felt more productive than it would have been to rewrite the
same program in Java, even with several extra years of Java experience
acquired since writing the first version.

举个例子，在一次假期里，我差不多在 Lisp
上花了一个星期的时间，目标是实现一个基于遗传算法用来下围棋的程序系统——我以前做
Java 程序员的时候已经写过了。虽然我那时的 Common
Lisp 知识极其有限，还要不时地查询基本函数的用法，但我还是能感觉到比用
Java 重写同样的程序来得顺手——尽管从编写该程序的最初版本以来，我又多了几年的
Java 经验。

A similar experiment led to the library I'll discuss in
Chapter 24. Early in my time at WebLogic I had written a library, in
Java, for taking apart Java class files. It worked, but the code was a
bit of a mess and hard to modify or extend. I had tried several times,
over the years, to rewrite that library, thinking that with my
ever-improving Java chops I'd find some way to do it that didn't bog
down in piles of duplicated code. I never found a way. But when I
tried to do it in Common Lisp, it took me only two days, and I ended
up not only with a Java class file parser but with a general-purpose
library for taking apart any kind of binary file. You'll see how that
library works in Chapter 24 and use it in Chapter 25 to write a parser
for the ID3 tags embedded in MP3 files.

类似的经历还产生了我将在第 24 章里讨论的一个库。我以前在 WebLogic
的时候曾经用 Java 写了一个用来解析 Java
类文件的库。虽然库可以正常使用，但是代码有点乱，并且难以修改或扩展。几年来我曾多次重写这个库，并期望凭借日益提高的
Java 技巧可以找到某种方式来消除其中大量的重复代码，可惜从未成功。但当我改用
Common Lisp 做这件事时，我只花了两天时间，最后不但得到了一个 Java
类文件的解析器，而且还产生了一个可用于解析任何二进制文件的通用库。第
24 章将讨论这个库的工作原理，第 25 章会用它写一个 MP3 文件的内嵌 ID3
标签的解析器。
