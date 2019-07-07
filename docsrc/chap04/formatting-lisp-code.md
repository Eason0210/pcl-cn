# Formatting Lisp Code（格式化 Lisp 代码）

While code formatting is, strictly speaking, neither a syntactic nor a
semantic matter, proper formatting is important to reading and writing
code fluently and idiomatically. The key to formatting Lisp code is to
indent it properly. The indentation should reflect the structure of
the code so that you don't need to count parentheses to see what goes
with what. In general, each new level of nesting gets indented a bit
more, and, if line breaks are necessary, items at the same level of
nesting are lined up. Thus, a function call that needs to be broken up
across multiple lines might be written like this:

严格说起来，代码格式化既不是句法层面也不是语法层面上的事情，好的格式化对于阅读和编写流利而又地道的代码而言非常重要。格式化
Lisp 代码的关键在于正确缩进它。这一缩进应当反映出代码结构，这样就不需要通过数括号来查看代码究竟写到哪儿了。一般而言，每一个新的嵌套层次都需要多缩进一点儿，并且如果折行是必需的，位于同一个嵌套层次的项应当按行对齐。这样，一个需要跨越多行的函数调用可能会被写成这样：

```lisp
(some-function arg-with-a-long-name
               another-arg-with-an-even-longer-name)
```

Macro and special forms that implement control constructs are
typically indented a little differently: the "body" elements are
indented two spaces relative to the opening parenthesis of the
form. Thus:

那些实现控制结构的宏和特殊形式在缩进上稍有不同：“主体”
元素相对于整个形式的开放括号缩进两个空格。就像这样：

```lisp
(defun print-list (list)
  (dolist (i list)
    (format t "item: ~a~%" i)))
```

However, you don't need to worry too much about these rules because a
proper Lisp environment such as SLIME will take care of it for you. In
fact, one of the advantages of Lisp's regular syntax is that it's
fairly easy for software such as editors to know how to indent
it. Since the indentation is supposed to reflect the structure of the
code and the structure is marked by parentheses, it's easy to let the
editor indent your code for you.

尽管如此，但也不需要太担心这些规则，因为一个像 SLIME 这样的优秀 Lisp
环境将会帮你做到这点。事实上，Lisp
正则语法的优势之一就在于，它可以让诸如编辑器这样的软件相对容易地知道应当如何缩进。由于缩进的本意是反映代码的结构，而结构是由括号来标记的，因此很容易让编辑器帮你缩进代码。

In SLIME, hitting Tab at the beginning of each line will cause it to
be indented appropriately, or you can re-indent a whole expression by
positioning the cursor on the opening parenthesis and typing `C-M-q`. Or
you can re-indent the whole body of a function from anywhere within it
by typing `C-c M-q`.

在 SLIME 中，在每行开始处按下 Tab
键将导致该行被适当地缩进，或者也可以通过将光标放置在一个开放的括号上并键入
`C-M-q` 来重新缩进整个表达式。或者还可以在函数内部的任何位置通过键入
`C-c M-q` 来重新缩进整个函数体。

Indeed, experienced Lisp programmers tend to rely on their editor
handling indenting automatically, not just to make their code look
nice but to detect typos: once you get used to how code is supposed to
be indented, a misplaced parenthesis will be instantly recognizable by
the weird indentation your editor gives you. For example, suppose you
were writing a function that was supposed to look like this:

的确，有经验的 Lisp
程序员们倾向于依赖的编辑器来自动处理缩进，这样不但可以确保代码美观，还可以检测笔误：一旦熟悉了代码该如何缩进，那么一个错误放置的括号就将立即由于编辑器所给出的奇怪缩进而被发现。例如，假设要编写一个如下所示函数：

```lisp
(defun foo ()
  (if (test)
    (do-one-thing)
    (do-another-thing)))
```

Now suppose you accidentally left off the closing parenthesis after
test. Because you don't bother counting parentheses, you quite likely
would have added an extra parenthesis at the end of the DEFUN form,
giving you this code:

现在假设你不小心忘记了 `test`
后面的闭合括号。如果不去数括号的话，那么很可能就会在 **DEFUN**
形式的结尾处添加一个额外的括号，从而得到下面的代码：

```lisp
(defun foo ()
  (if (test
    (do-one-thing)
    (do-another-thing))))
```

However, if you had been indenting by hitting Tab at the beginning of
each line, you wouldn't have code like that. Instead you'd have this:

尽管如此，如果一直都在每行的开始处按 Tab
来缩进的话，就不会得到这样的代码。相反你将得到如下的代码：

```lisp
(defun foo ()
  (if (test
       (do-one-thing)
       (do-another-thing))))
```

Seeing the then and else clauses indented way out under the condition
rather than just indented slightly relative to the IF shows you
immediately that something is awry.

看到 then 和 else
子句被缩进到了条件语句的位置，而不是仅仅相对于IF稍微缩进了一点，你将立即看出有错误发生。

Another important formatting rule is that closing parentheses are
always put on the same line as the last element of the list they're
closing. That is, don't write this:

另一个重要的格式化规则是，闭合的括号总是位于与它们所闭合的列表最后一个元素相同的行。也就是说，不要写成这样：

```lisp
(defun foo ()
  (dotimes (i 10)
    (format t "~d. hello~%" i)
  )
)
```

but instead write this:

而一定要写成这样：

```lisp
(defun foo ()
  (dotimes (i 10)
    (format t "~d. hello~%" i)))
```

The string of `)))`s at the end may seem forbidding, but as long your
code is properly indented the parentheses should fade away--no need to
give them undue prominence by spreading them across several lines.

结尾处的 `)))`
可能看起来令人生畏，但是一旦代码缩进正确，那么括号的意义就不存在了——没有必要通过将它们分散在多行来加以突出。

Finally, comments should be prefaced with one to four semicolons
depending on the scope of the comment as follows:

最后，注释应该根据其适用范围被前置一到四个分号，如同下面所说明的：

```lisp
;;;; Four semicolons are used for a file header comment.（四个分号用于文件头注释。）

;;; A comment with three semicolons will usually be a paragraph
;;; comment that applies to a large section of code that follows,
;;; （一个带有三个分号的注释将通常作为段落注释应用到接下来的一大段代码上）

(defun foo (x)
  (dotimes (i x)
    ;; Two semicolons indicate this comment applies to the code
    ;; that follows. Note that this comment is indented the same
    ;; as the code that follows.
    ;; 两个分号说明该注释应用于接下来的代码上。
    ;; 注意到该注释处在与其所应用的代码相同的缩进上。
    (some-function-call)
    (another i)              ; this comment applies to this line only（本注释仅用于此行）
    (and-another)            ; and this is for this line（这个也是一样）
    (baz)))
```

Now you're ready to start looking in greater detail at the major
building blocks of Lisp programs, functions, variables, and
macros. Up next: functions.
  
现在可以开始了解 Lisp
的主要程序构造的更多细节了：函数、变量和宏。下一章先来看看函数。
