C语言堆与线相关知识
===

1. 函数调用过程是如何压栈及出栈的？

    <details>
      <summary>参考答案</summary>

      每个函数都有一段空间，存储其入参、本地变量及其它临时变量（如函数返回地址等），该段空间称为函数调用栈(call stack)。调用栈是一个栈数据结构，其维护由程序自行处理。
      函数调用过程的压栈、出栈的具体操作与操作系统及CPU架构相关，下面介绍一般过程：
      1. 保存寄存器中的函数返回地址（caller的下一条语句的执行地址）、栈顶地址到栈上
      2. 栈顶指针偏移（由高地址向低地址移动）
      3. 入参压栈
      4. 局部变量压栈
      5. 执行函数代码
      6. 退出时恢复caller的函数返回地址、栈顶指针地址到寄存器中

      参考资料：
      - [C语言中的"函数调用栈"一定要弄懂！](https://z.itpub.net/article/detail/50503CAA1CDDA808A925D5758BD1B0A4)
      - [call stack](https://en.wikipedia.org/wiki/Call_stack)
      - [Stack frames](https://people.cs.rutgers.edu/~pxk/419/notes/frames.html)
      - [A Guide to ARM64 / AArch64 Assembly on Linux with Shellcodes and Cryptography](https://modexp.wordpress.com/2018/10/30/arm64-assembly/)
    </details>
