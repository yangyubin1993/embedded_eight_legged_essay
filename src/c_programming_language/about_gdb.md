gdb使用相关知识
===

1. 什么是`gdb`？
   <details>
      <summary>参考答案</summary>

	  `gdb`全称为`GNU Debugger`，是可以运行于多种类Unix平台的程序调试软件。类似的软件还有`lldb`，`lldb`常用于`macos`。

	  参考资料：
	  - [GNU Debugger](https://en.wikipedia.org/wiki/GNU_Debugger)
    </details>

2. gdb常见命令有哪些？
   
	<details>
      <summary>参考答案</summary>

	  gdb的常见命令有：
	  1. help: 获取gdb命令帮助
	  2. help `<command>`: 获取特定gdb命令的帮助
	  3. run: 运行到下个断点或程序结束
	  4. step: 单步（逐语句）调试，会进入到函数内部执行
	  5. next: 单步（逐语句）调试，但不会进入到函数内部执行
	  6. finish: 结束当前函数或循环
	  7. continue: 执行到下个断点或程序结束
	  8. up `<N>`: 往栈顶移动`N`帧，`N`默认为1
	  9. down `<N>`: 往栈顶移动`N`帧，`N`默认为1
	  10. list: 打印当前点附近的代码
	  11. print `<name>`: 打印名为`name`的变量值
	  12. print *`<name>`: 打印`name`指针指向的值
	  13. print/x `<name>`: 以16进制打印`name`的值
	  14. print `<name>`@`<n>`: 打印以`name`为起始地址的`n`个值
	  15. break `<name>`: 在函数`name`处设置断点
	  16. break `<num>`: 在行`num`处设置断点
	  17. disable 1: 去使能断点1
	  18. enable 1: 使能断点1
	  19. delete 1: 删除断点1
	  20. delete: 删除所有断点
	  21. condition 1 `<expr>`: 断点1的停止条件为表达式`expr`为true
	  22. condition 1: 删除断点1的所有条件
	  23. info break: 显示所有的断点信息
	  24. backtrace: 查看栈信息
	  25. display `<name>`: 始终显示变量`name`的值
	  26. undisplay `<name>`: 取消跟踪`name`的值
	  27. watch `<expr>`: 监视`expr`的值，一旦有变化就暂停程序

	  参考资料：
	  - [Useful commands in gdb](https://ccrma.stanford.edu/~jos/stkintro/Useful_commands_gdb.html)
  
    </details>

3. gdb调试的原理是？

	<details>
      <summary>参考答案</summary>

	  `gdb`使用系统调用`ptrace`(process trace)去观察和控制其它进程的执行、检查和修改其它进程的内存和寄存器。

	  参考资料：
	  - [GNU Debugger](https://en.wikipedia.org/wiki/GNU_Debugger)
	  - [gdb 的基本工作原理](http://www.kgdb.info/wp-content/uploads/2011/04/GdbPrincipleChinese.pdf)
  
    </details>

4. 如何调试`多进程`程序？

	<details>
      <summary>参考答案</summary>

    </details>

5. 如何调试`多线程`程序？

	<details>
      <summary>参考答案</summary>

    </details>

6. 什么是`core`文件？有什么作用？

	<details>
      <summary>参考答案</summary>

    </details>