# Saving Your Work（保存工作成果）

You could argue that this is a complete "hello, world" program of
sorts. However, it still has a problem. If you exit Lisp and restart,
the function definition will be gone. Having written such a fine
function, you'll want to save your work.

你可能会争辩说这就是一个完整的“hello, world”程序了。但还有一个问题。如果退出
Lisp 然后重启，函数定义将会丢失。这么好的一个函数，你可能会想要保存下来。

Easy enough. You just need to create a file in which to save the
definition. In Emacs you can create a new file by typing `C-x C-f` and
then, when Emacs prompts you, entering the name of the file you want
to create. It doesn't matter particularly where you put the file. It's
customary to name Common Lisp source files with a `.lisp` extension,
though some folks use .cl instead.

而这很简单。只需创建一个文件，然后把定义保存在里面即可。在 Emacs
中可以通过输入 `C-x C-f` 来创建一个新文件，然后根据
Emacs 的提示输入文件的名字。文件保存的位置并不重要。Common
Lisp 源文件习惯上带有 `.lisp` 扩展名，尽管有些人用 `.cl` 来代替。

Once you've created the file, you can type the definition you
previously entered at the REPL. Some things to note are that after you
type the opening parenthesis and the word **DEFUN**, at the bottom of
the Emacs window, SLIME will tell you the arguments expected. The
exact form will depend somewhat on what Common Lisp implementation
you're using, but it'll probably look something like this:

一旦创建了文件，就可以向其中写入之前在 REPL
里输入过的定义。需要注意的是，在输入了开放括号和单词 **DEFUN**
以后，在 Emacs 窗口的底部，SLIME
将会提示它所期待的参数。具体的输出将取决于所使用的具体 Common Lisp
实现，但其形式可能会如下所示：

```lisp
(defun name varlist &rest body)
```

The message will disappear as you start to type each new element but
will reappear each time you enter a space. When you're entering the
definition in the file, you might choose to break the definition
across two lines after the parameter list. If you hit Return and then
Tab, SLIME will automatically indent the second line appropriately,
like this:

在开始输入每一个新的列表元素时，这个信息就会消失，但当每次输入了空格以后，它又会重新出现。在文件中输入这个定义的时候，你可能选择将函数从形参列表那里打断成两行。如果输入回车然后按
Tab 键，SLIME 将自动把第二行缩进到合适的位置，如下所示：

```lisp
(defun hello-world ()
  (format t "hello, world"))
```

SLIME will also help match up the parentheses--as you type a closing
parenthesis, it will flash the corresponding opening parenthesis. Or
you can just type `C-c C-q` to invoke the command
`slime-close-parens-at-point`, which will insert as many closing
parentheses as necessary to match all the currently open parentheses.

SLIME 也会帮助匹配括号——当输入了闭合括号时，它将闪烁显示对应的开放括号。或者也可以输入
`C-c C-q` 来调用命令 `slime-close-parens-at-point`，它将插入必要数量的闭合括号以匹配当前的所有开放括号。

Now you can get this definition into your Lisp environment in several
ways. The easiest is to type `C-c C-c` with the cursor anywhere in or
immediately after the **DEFUN** form, which runs the command
`slime-compile-defun`, which in turn sends the definition to Lisp to be
evaluated and compiled. To make sure this is working, you can make
some change to hello-world, recompile it, and then go back to the
REPL, using `C-c C-z` or `C-x b`, and call it again. For instance, you
could make it a bit more grammatical.

可用几种方式将这个定义输入到 Lisp 环境中。最简单的是，当光标位于 **DEFUN**
定义内部的任何位置或者刚好在其后面时，输入 `C-c C-c`，这将启动
`slime-compile-defun` 命令，将当前定义发给 Lisp
进行求值并编译。为了确认这个过程有效，你可以对 `hello-world`
作些修改，重新编译它然后回到 REPL，使用 `C-c C-z` 或者
`C-x b` 再次调用它。例如，你可以使其更合乎语法。

```lisp
(defun hello-world ()
  (format t "Hello, world!"))
```

Next, recompile with `C-c C-c` and then type `C-c C-z` to switch to the
REPL to try the new version.

接下来，用 `C-c C-c` 进行重新编译，然后输入 `C-c C-z` 来切换到 REPL
试一下新版本。

```
CL-USER> (hello-world)
Hello, world!
NIL
```

You'll also probably want to save the file you've been working on; in
the `hello.lisp` buffer, type `C-x C-s` to invoke the Emacs command
save-buffer.

你将可能需要保存工作文件。在 `hello.lisp` 缓冲区里，输入 `C-x C-s` 可以启动
Emacs 命令 `save-buffer`。

Now to try reloading this function from the source file, you'll need
to quit Lisp and restart. To quit you can use a SLIME shortcut: at the
REPL, type a comma. At the bottom of the Emacs window, you will be
prompted for a command. Type `quit` (or `sayoonara`), and then hit
Enter. This will quit Lisp and close all the buffers created by SLIME
such as the REPL buffer. Now restart SLIME by typing `M-x slime`.

现在尝试从源文件中重新加载这个函数，这需要退出并重启 Lisp
环境。执行退出操作可以使用一个 SLIME 快捷键：在 REPL
中输入一个逗号。在 Emacs 窗口底部，将提示你输入一个命令。输入
`quit`（或 `sayoonara`），然后按回车。这将退出 Lisp
并且关闭所有 SLIME 创建的缓冲区，包括 REPL 缓冲区。 现在用 `M-x slime`
重启 SLIME。

Just for grins, you can try to invoke `hello-world`.

可以顺便试试直接调用 `hello-world`。

```
CL-USER> (hello-world)
```

At that point SLIME will pop up a new buffer that starts with something that looks like this:

此时 SLIME 将弹出一个新的缓冲区并带有类似下面的内容：

```
attempt to call `HELLO-WORLD' which is an undefined function.
   [Condition of type UNDEFINED-FUNCTION]

Restarts:
  0: [TRY-AGAIN] Try calling HELLO-WORLD again.
  1: [RETURN-VALUE] Return a value instead of calling HELLO-WORLD.
  2: [USE-VALUE] Try calling a function other than HELLO-WORLD.
  3: [STORE-VALUE] Setf the symbol-function of HELLO-WORLD and call it again.
  4: [ABORT] Abort handling SLIME request.
  5: [ABORT] Abort entirely from this process.

Backtrace:
  0: (SWANK::DEBUG-IN-EMACS #<UNDEFINED-FUNCTION @ #x716b082a>)
  1: ((FLET SWANK:SWANK-DEBUGGER-HOOK SWANK::DEBUG-IT))
  2: (SWANK:SWANK-DEBUGGER-HOOK #<UNDEFINED-FUNCTION @ #x716b082a> #<Function SWANK-DEBUGGER-HOOK>)
  3: (ERROR #<UNDEFINED-FUNCTION @ #x716b082a>)
  4: (EVAL (HELLO-WORLD))
  5: (SWANK::EVAL-REGION "(hello-world)
  " T)
```
  
Blammo! What happened? Well, you tried to invoke a function that
doesn't exist. But despite the burst of output, Lisp is actually
handling this situation gracefully. Unlike Java or Python, Common
Lisp doesn't just bail--throwing an exception and unwinding the
stack. And it definitely doesn't dump core just because you tried to
invoke a missing function. Instead Lisp drops you into the
debugger. 

天哪！发生了什么事？原来，你试图调用了一个不存在的函数。不过尽管输出了很多东西，Lisp
实际上正在很好地处理这一情况。跟 Java 或者 Python 不同，Common
Lisp 不会只是放弃——抛出一个异常并从栈上退回，而且它也绝对不会仅仅因为调用了一个不存在的函数就开始做核心转储（core
dump）。事实上 Lisp 会把你带进调试器。

While you're in the debugger you still have full access to Lisp, so
you can evaluate expressions to examine the state of our program and
maybe even fix things. For now don't worry about that; just type `q` to
exit the debugger and get back to the REPL. The debugger buffer will
go away, and the REPL will show this:

当身处调试器之中时，你仍然拥有对 Lisp 的完全访问权限，所以可以通过求值表达式来检查我们程序的状态，甚至可以直接修复一些东西。不过目前先别担心它们。直接输入
`q` 退出调试器，然后回到 REPL 里。调试器缓冲区将会消失，而 REPL 将显示：

```
CL-USER> (hello-world)
; Evaluation aborted
CL-USER>
```

There's obviously more that can be done from within the debugger than
just abort--we'll see, for instance, in Chapter 19 how the debugger
integrates with the error handling system. For now, however, the
important thing to know is that you can always get out of it, and back
to the REPL, by typing `q`.

相比直接中止调试器，在它里面显然可以做更多的事情——例如我们将在第 19
章里看到调试器是如何与错误处理系统集成在一起的。尽管如此，目前最重要的是要知道总是可以通过按
`q` 来退出它并回到 REPL 里。

Back at the REPL you can try again. Things blew up because Lisp didn't
know the definition of hello-world. So you need to let Lisp know about
the definition we saved in the file hello.lisp. You have several ways
you could do this. You could switch back to the buffer containing the
file (type `C-x b` and then enter hello.lisp when prompted) and
recompile the definition as you did before with `C-c C-c`. Or you can
load the whole file, which would be a more convenient approach if the
file contained a bunch of definitions, using the LOAD function at the
REPL like this:

回到 REPL 里可以再试一次。问题在于 Lisp 不知道 `hello-world`
的定义，因此你需要让 Lisp 知道我们保存在 `hello.lisp`
文件中的定义。有几种方式可以做到这一点。可以切换回含有那个文件的缓冲区（使用
`C-x b` 在其提示时输入 `hello.lisp`），然后就像之前那样用
`C-c C-c` 重新编译那个定义。或者你可以加载整个文件，当文件里含有大量定义时，这将更加便利，在
REPL 里像这样使用 **LOAD** 函数：

```
CL-USER> (load "hello.lisp")
; Loading /home/peter/my-lisp-programs/hello.lisp
T
```

The **T** means everything loaded correctly. Loading a file with
**LOAD** is essentially equivalent to typing each of the expressions
in the file at the REPL in the order they appear in the file, so after
the call to LOAD, hello-world should be defined:

那个 **T** 表示文件被正确加载了。 使用 **LOAD**
加载一个文件，本质上等价于以文件中出现的顺序在 REPL
下逐个输入每一个表达式，因此在调用了 **LOAD** 之后，`hello-world` 就应该有定义了：

```
CL-USER> (hello-world)
Hello, world!
NIL
```

Another way to load a file's worth of definitions is to compile the
file first with **COMPILE-FILE** and then **LOAD** the resulting compiled
file, called a FASL file, which is short for fast-load
file. **COMPILE-FILE** returns the name of the FASL file, so we can
compile and load from the REPL like this:

另一种加载文件中有用定义的方法是先用 **COMPILE-FILE** 编译，然后再用 **LOAD**
加载编译后产生的文件，也就是 FASL 文件——快速加载文件（fast-load file）的简称。**COMPILE-FILE**
将返回 FASL 文件的名字，所以我们可以在 REPL 里像下面这样进行编译和加载：

```lisp
CL-USER> (load (compile-file "hello.lisp"))
;;; Compiling file hello.lisp
;;; Writing fasl file hello.fasl
;;; Fasl write complete
; Fast loading /home/peter/my-lisp-programs/hello.fasl
T
```

SLIME also provides support for loading and compiling files without
using the REPL. When you're in a source code buffer, you can use
`C-c C-l` to load the file with `slime-load-file`. Emacs will prompt for the
name of a file to load with the name of the current file already
filled in; you can just hit Enter. Or you can type `C-c C-k` to compile
and load the file represented by the current buffer. In some Common
Lisp implementations, compiling code this way will make it quite a bit
faster; in others, it won't, typically because they always compile
everything.

SLIME 还提供了不需要使用 REPL 来加载和编译文件的支持。在一个源代码缓冲区时，你可以使用
`C-c C-l` 调用命令 `slime-load-file` 来加载文件。Emacs
将会提示你给出要加载的文件名，同时将当前的文件名作为默认值，直接回车就可以了。或者可以输入
`C-c C-k` 来编译并加载那个当前缓冲区所关联的文件。在一些
Common Lisp
实现里，对代码进行编译将使其速度更快一些；在其他实现里可能不会，因为它们总是编译所有东西。

This should be enough to give you a flavor of how Lisp programming
works. Of course I haven't covered all the tricks and techniques yet,
but you've seen the essential elements--interacting with the REPL
trying things out, loading and testing new code, tweaking and
debugging. Serious Lisp hackers often keep a Lisp image running for
days on end, adding, redefining, and testing bits of their program
incrementally.

这些内容应该足够给你一个关于 Lisp
编程如何工作的大致印象了。当然我还没有涉及所有的技术和窍门，但你已经见到其本质要素了——通过与
REPL 的交互来尝试一些东西，加载和测试新代码，调整和调试它们。资深的
Lisp 黑客们经常会保持一个 Lisp
映像日复一日地运行，不断地添加、重定义和测试他们的程序。

Also, even when the Lisp app is deployed, there's often still a way to
get to a REPL. You'll see in Chapter 26 how you can use the REPL and
SLIME to interact with the Lisp that's running a Web server at the
same time as it's serving up Web pages. It's even possible to use
SLIME to connect to a Lisp running on a different machine, allowing
you--for instance--to debug a remote server just like a local one.

同样地，甚至当 Lisp 程序被部署以后，往往仍有一种方式可以进入 REPL。第 26
章介绍如何使用 REPL 和 SLIME 来跟正在运行一个 Web 服务器的 Lisp
进行交互，同时它还在伺服 Web 页面。甚至有可能用 SLIME
连接到运行在另一台不同机器里的
Lisp，从而允许你（比如说）像本地环境那样去调试一个远程服务器。

An even more impressive instance of remote debugging occurred on
NASA's 1998 Deep Space 1 mission. A half year after the space craft
launched, a bit of Lisp code was going to control the spacecraft for
two days while conducting a sequence of experiments. Unfortunately, a
subtle race condition in the code had escaped detection during ground
testing and was already in space. When the bug manifested in the
wild--100 million miles away from Earth--the team was able to diagnose
and fix the running code, allowing the experiments to complete. One
of the programmers described it as follows:

一个更加令人印象深刻的案例是 1998 年发生在 NASA 的 Deep Space 1
号任务中的远程调试。在宇宙飞船升空半年以后，一小段 Lisp
代码正准备控制飞船以进行为期两天的一系列实验。不幸的是，代码里的一个难以察觉的竟态条件逃过了地面测试期间的检测并且已经升空了。当这个错误在距地球一亿英里外的地方出现时，地面团队得以诊断并修复了运行中的代码，使得实验顺利地完成。 一个程序员如此描述了这件事：

> Debugging a program running on a $100M piece of hardware that is 100
> million miles away is an interesting experience. Having a
> read-eval-print loop running on the spacecraft proved invaluable in
> finding and fixing the problem.

> 调试一个运行在一亿英里之外且价值一亿美元硬件上的程序是件有趣的经历。一个运行在宇宙飞船上的读-求值-打印循环，在查找和修复这个问题的过程中，真是无价之宝啊。

You're not quite ready to send any
Lisp code into deep space, but in the next chapter you'll take a crack
at writing a program a bit more interesting than "hello, world."

你还没有准备好将任何 Lisp
代码发送到太空，不过在接下来一章里，你就将亲身参与编写一个比“hello,
world”更有趣一点儿的程序了。
