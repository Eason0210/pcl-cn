# Practical: A Portable Pathname Library（实践：可移植路径名库）

As I discussed in the previous chapter, Common Lisp provides an
abstraction, the pathname, that's supposed to insulate you from the
details of how different operating systems and file systems name
files. Pathnames provide a useful API for manipulating names as names,
but when it comes to the functions that actually interact with the
file system, things get a bit hairy.

如同我在前面章节里讨论的那样，Common Lisp
提供了一种称为路径名的抽象，这样一来，你就不用顾忌不同操作系统和文件系统在文件命名方式上的差异。路径名提供了一个有用的
API 来管理作为路径的名字，但是当它涉及实际与文件系统交互的函数时，事情就会变得有些复杂。

The root of the problem, as I mentioned, is that the pathname
abstraction was designed to represent filenames on a much wider
variety of file systems than are commonly used now. Unfortunately, by
making pathnames abstract enough to account for a wide variety of file
systems, Common Lisp's designers left implementers with a fair number
of choices to make about how exactly to map the pathname abstraction
onto any particular file system. Consequently, different implementers,
each implementing the pathname abstraction for the same file system,
just by making different choices at a few key junctions, could end up
with conforming implementations that nonetheless provide different
behavior for several of the main pathname-related functions.

如同我提到的，问题的根源在于，路径名抽象被设计用来表示比当今常用的文件系统更加广泛的系统上的文件名。不幸的是，为了让路径名足够抽象从而可以应用于广泛的文件系统，Common
Lisp
的设计者们留给了实现者们大量的选择空间，来决定究竟如何将路径名抽象映射到任何特定文件系统上。这样带来的结果是，不同的实现者虽然在相同的文件系统上实现路径名抽象，但在一些关键点上却做出了不同的选择，从而导致遵循标准的实现在一些主要的路径名相关函数上不可避免地提供了不同的行为。

However, one way or another, all implementations provide the same
basic functionality, so it's not too hard to write a library that
provides a consistent interface for the most common operations across
different implementations. That's your task for this chapter. In
addition to giving you several useful functions that you'll use in
future chapters, writing this library will give you a chance to learn
how to write code that deals with differences between

然而，所有的实现都以这样或那样的方式提供了相同的基本功能，因此你可以写一个库，对多数跨越不同实现的常见操作提供一致的接口。这就是你在本章中的任务。编写这个库，你不但可以获得后续几章将会用到的几个有用的函数，还可以有机会学习如何编写处理不同
Lisp 实现间有区别的代码。
