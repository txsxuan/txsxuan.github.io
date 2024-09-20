# 更适合酥老师的GDB教程*

今晚浅浅学下GDB，先看下文档。
```
       break [file:][function|line]
           Set a breakpoint at function or line (in file).

       run [arglist]
           Start your program (with arglist, if specified).

       bt  Backtrace: display the program stack.

       print expr
           Display the value of an expression.

       c   Continue running your program (after stopping, e.g. at a
           breakpoint).

       next
           Execute next program line (after stopping); step over any function
           calls in the line.

       edit [file:]function
           look at the program line where it is presently stopped.

```
咳咳，文档看不明白，怎么办！快来使用酥语言翻译（）
俗话说，实践！是检验真理的唯一标准哈，实际上gdb的使用更多的还是通过实践。不过这是后话了，因为笔者刚准备写的时候已经是晚上十一点半了，晚安，明天继续。