# But I learned Lisp Once, And IT Wasn't Like what you're describing（我曾经学过 Lisp，不过跟你所描述的不太一样）

If you've used Lisp in the past, you may have ideas about what "Lisp"
is that have little to do with Common Lisp. While Common Lisp
supplanted most of the dialects it's descended from, it isn't the only
remaining Lisp dialect, and depending on where and when you were
exposed to Lisp, you may very well have learned one of these other
dialects.

如果你以前用过 Lisp，你对 Lisp 的认识很可能对学习 Common Lisp
没什么帮助。尽管 Common Lisp 取代了大多数它所继承下来的方言，但它并非仅存的
Lisp 方言。你要清楚自己是在何时何地认识 Lisp 的，很有可能你学的是某种其他方言。

Other than Common Lisp, the one general-purpose Lisp dialect that
still has an active user community is Scheme. Common Lisp borrowed a
few important features from Scheme but never intended to replace it.

除了 Common Lisp 以外，另一种仍然有着活跃用户群的通用 Lisp 方言是 Scheme。
Common Lisp 从 Scheme 那里吸收了一些重要的特性，但从未试图取代它。

Originally designed at M.I.T., where it was quickly put to use as a
teaching language for undergraduate computer science courses, Scheme
has always been aimed at a different language niche than Common
Lisp. In particular, Scheme's designers have focused on keeping the
core language as small and as simple as possible. This has obvious
benefits for a teaching language and also for programming language
researchers who like to be able to formally prove things about
languages.

Scheme 最早在 MIT
被设计出来，然后很快用作本科计算机科学课程的教学语言，它一直被定位成一种与
Common Lisp 有所不同的语言。特别是 Scheme
的设计者们将注意力集中在使其语言核心尽可能地小而简单。这对作为教学语言来说非常有用，编程语言研究者们也很容易形式化地证明语言本身的有关命题。

It also has the benefit of making it relatively easy to understand the
whole language as specified in the standard. But, it does so at the
cost of omitting many useful features that are standardized in Common
Lisp. Individual Scheme implementations may provide these features in
implementation-specific ways, but their omission from the standard
makes it harder to write portable Scheme code than to write portable
Common Lisp code.

这样设计的另一个好处是使得通过标准规范理解整个语言变得相对简单。但是，这样做带来的问题是缺失了许多在
Common Lisp 里已经标准化了的有用特性。个别的 Scheme
实现者可能以特定的实现方式提供了这些特性，但它们在标准中的缺失则使得编写可移植的
Scheme 代码比编写可移植的 Common Lisp 代码更加困难。

Scheme also emphasizes a functional programming style and the use of
recursion much more than Common Lisp does. If you studied Lisp in
college and came away with the impression that it was only an academic
language with no real-world application, chances are you learned
Scheme. This isn't to say that's a particularly fair characterization
of Scheme, but it's even less applicable to Common Lisp, which was
expressly designed to be a real-world engineering language rather than
a theoretically "pure" language.

Scheme 同样强调函数式的编程风格，并且使用了比 Common Lisp
更多的递归。如果在大学里学过 Lisp
并且感觉它只是一种没有现实应用的学术语言，那你八成是学了
Scheme。当然，说 Scheme
具有这样的特征并不是很公正，只不过同样的说法用在 Common Lisp
身上更加不合适罢了，后者专门被设计成真实世界的工程语言，而不是一种理论上的“纯”语言。

If you've learned Scheme, you should also be aware that a number of
subtle differences between Scheme and Common Lisp may trip you
up. These differences are also the basis for several perennial
religious wars between the hotheads in the Common Lisp and Scheme
communities. I'll try to point out some of the more important
differences as we go along.

如果你已经学过了 Scheme，就应该注意 Scheme 和 Common Lisp
之间的许多细微差别可能会使人犯错。这些差别也是 Common Lisp 和
Scheme 社区的狂热分子之间一些长期信仰之争的导火索。日后随着讨论的深入，我将指出其中最重要的差别。

Two other Lisp dialects still in widespread use are Elisp, the
extension language for the Emacs editor, and Autolisp, the extension
language for Autodesk's AutoCAD computer-aided design tool. Although
it's possible more lines of Elisp and Autolisp have been written than
of any other dialect of Lisp, neither can be used outside their host
application, and both are quite old-fashioned Lisps compared to either
Scheme or Common Lisp. If you've used one of these dialects, prepare
to hop in the Lisp time machine and jump forward several decades.

另外两种仍然广泛使用的 Lisp 方言是 Elisp 和 Autolisp。Emacs 是 Emacs
编辑器的扩展语言，而 Autolisp 是 Autodesk 的 AutoCAD
计算机辅助设计工具的扩展语言。尽管用 Elisp 和 Autolisp
可能已经写出了超过任何其他方言的代码行数，但它们都不能用在各自的宿主应用程序之外，而且它们无论与
Scheme 还是 Common Lisp 相比都是相当过时的 Lisp
方言了。如果你曾经用过这些方言的一种，就需要做好准备，你可能要在 Lisp
时间机器里向前跳跃几十年了。
