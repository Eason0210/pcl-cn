# Better Result Reporting（更好的结果输出）

As long as you have only one test function, the current result
reporting is pretty clear. If a particular test case fails, all you
have to do is find the test case in the check form and figure out why
it's failing. But if you write a lot of tests, you'll probably want to
organize them somehow, rather than shoving them all into one
function. For instance, suppose you wanted to add some test cases for
the `*` function. You might write a new test function.

由于只有一个测试函数，所以当前的结果输出是相当清晰的。如果一个特定的测试用例失败了，那么只需在
`check` 形式中找到那个测试用例并找出其失败原因即可。但如果编写了大量测试，会可能就要以某种方式将它们组织起来，而不是将它们全部塞进一个函数里。例如，假设想要对
`*` 函数添加一些测试用例，则可以写一个新的测试函数。

```lisp
(defun test-* ()
  (check
    (= (* 2 2) 4)
    (= (* 3 5) 15)))
```

Now that you have two test functions, you'll probably want another
function that runs all the tests. That's easy enough.

现在有了两个测试函数，你可能还想用另一个函数来运行所有测试，这也相当简单。

```lisp
(defun test-arithmetic ()
  (combine-results
   (test-+)
   (test-*)))
```

In this function you use combine-results instead of check since both
`test-+` and `test-*` will take care of reporting their own results. When
you run `test-arithmetic`, you'll get the following results:

这个函数使用 `combine-results` 来代替 `check`，因为 `test-+`
和 `test-*` 都将分别汇报它们自己的结果。运行 `test-arithmetic` 将得到下列结果：

```lisp
CL-USER> (test-arithmetic)
pass ... (= (+ 1 2) 3)
pass ... (= (+ 1 2 3) 6)
pass ... (= (+ -1 -3) -4)
pass ... (= (* 2 2) 4)
pass ... (= (* 3 5) 15)
T
```

Now imagine that one of the test cases failed and you need to track
down the problem. With only five test cases and two test functions, it
won't be too hard to find the code of the failing test case. But
suppose you had 500 test cases spread across 20 functions. It might be
nice if the results told you what function each test case came from.

现在假设其中一个测试用例失败了并且需要跟踪该问题。在只有五个测试用例和两个测试函数的情况下，找出失败测试用例的代码并不太困难。但假如有
500 个测试用例分散在 20
个函数里，如果测试结果可以显示每个测试用例来自什么函数就非常好了。

Since the code that prints the results is centralized in
report-result, you need a way to pass information about what test
function you're in to `report-result`. You could add a parameter to
`report-result` to pass this information, but check, which generates the
calls to `report-result`, doesn't know what function it's being called
from, which means you'd also have to change the way you call check,
passing it an argument that it simply passes onto `report-result`.

由于打印结果的代码集中在 `report-result`
函数里，所以需用一种方式来当前所在测试函数的信息传递给 `report-result`。可以为
`report-result` 添加一个形参来传递这一信息，但生成 `report-result`
调用的 `check` 却并不知道它是从什么函数被调用的，这就意味着还需要改变调用
`check` 的方式，向其传递一个参数使其随后传给 `report-result`。

This is exactly the kind of problem dynamic variables were designed to
solve. If you create a dynamic variable that each test function binds
to the name of the function before calling check, then report-result
can use it without check having to know anything about it.

设计动态变量就是用于解决这类问题的。如果创建一个动态变量使得每个测试函数在调用
`check` 之前将其函数名绑定于其上，那么 `report-result`
就可以无需理会 `check` 来使用它了。

Step one is to declare the variable at the top level.

第一步是在最上层声明这个变量。

```lisp
(defvar *test-name* nil)
```

Now you need to make another tiny change to `report-result` to include
`*test-name*` in the **FORMAT** output.

现在你需要对 `report-result` 稍微改动一下，使其在FORMAT输出中包括 `*test-name*`。

```lisp
(format t "~:[FAIL~;pass~] ... ~a: ~a~%" result *test-name* form)
```

With those changes, the test functions will still work but will
produce the following output because `*test-name*` is never rebound:

有了这些改变，测试函数将仍然可以工作但将产生下面的输出，因为
`*test-name*` 从未被重新绑定：

```lisp
CL-USER> (test-arithmetic)
pass ... NIL: (= (+ 1 2) 3)
pass ... NIL: (= (+ 1 2 3) 6)
pass ... NIL: (= (+ -1 -3) -4)
pass ... NIL: (= (* 2 2) 4)
pass ... NIL: (= (* 3 5) 15)
T
```

For the name to be reported properly, you need to change the two test functions.

为了正确报告测试名称，需要改变两个测试函数。

```lisp
(defun test-+ ()
  (let ((*test-name* 'test-+))
    (check
      (= (+ 1 2) 3)
      (= (+ 1 2 3) 6)
      (= (+ -1 -3) -4))))

(defun test-* ()
  (let ((*test-name* 'test-*))
    (check
      (= (* 2 2) 4)
      (= (* 3 5) 15))))
```

Now the results are properly labeled.

现在结果被正确地标记了。

```lisp
CL-USER> (test-arithmetic)
pass ... TEST-+: (= (+ 1 2) 3)
pass ... TEST-+: (= (+ 1 2 3) 6)
pass ... TEST-+: (= (+ -1 -3) -4)
pass ... TEST-*: (= (* 2 2) 4)
pass ... TEST-*: (= (* 3 5) 15)
T
```
