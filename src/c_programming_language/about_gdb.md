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

	  `gdb`使用系统调用`ptrace`(process trace)去观察和控制其它进程的执行、检查和修改其它进程的内存和寄存器。`ptrace`的原型如下：

	  ```c
	  long ptrace(enum __ptrace_request request, pid_t pid, void *addr, void *data);
	  ```

      根据`ptrace`的manual手册，主要有两种跟踪进程的方式：
	  1. 父进程通过`fork`系统调用创建子进程，在子进程中作如下`ptrace`调用，然后再通过`execv`加载子进程程序。
   
	     ```c
		 ptrace(PTRACE_TRACEME, 0, 0, 0);
		 ```

	  2. 使用如下`ptrace`调用直接跟踪其它进程：
   
		 ```
		 ptrace(PTRACE_ATTACH, pid, 0, 0);
		 ```

	  当进程被跟踪时，每当有信号(signal)被分发给被跟踪的进程(tracee)时都会导致tracee暂停（`SIGKILL`是个例外）。进行跟踪的进程(tracer)通过`waitpid`系统调用(或类似的`wait`相关的系统调用)获知`tracee`被跟踪的情况。当tracee停止时，tracer还可以使用多种`ptrace request`去检查或修改`tracee`。

	  gdb断点（breakpoint）功能的软件实现原理是在指定位置插入断点指令（INT），当被调试的程序执行到断点位置时，产生`SIGTRAP`信号并转由gdb处理。
	
	  参考资料：
	  - [GNU Debugger](https://en.wikipedia.org/wiki/GNU_Debugger)
	  - [gdb 的基本工作原理](http://www.kgdb.info/wp-content/uploads/2011/04/GdbPrincipleChinese.pdf)
	  - [ptrace(2) — Linux manual page](https://man7.org/linux/man-pages/man2/ptrace.2.html)
	  - [自己动手写一个GDB｜设置断点（原理篇）](https://cloud.tencent.com/developer/article/2004708)
	  - [Breakpoint Handling](https://web.archive.org/web/20070304002738/http://sourceware.org/gdb/current/onlinedocs/gdbint_3.html#SEC10)
    </details>

4. 如何调试`多进程`程序？

	<details>
      <summary>参考答案</summary>

	  当我们使用`gdb`调试多进程程序时，如果进程使用`fork`创建了子进程，`gdb`仍会继续跟踪原来的进程，子进程正常执行。要想允许调试子进程，有两种方法：
	  1. 使用`attch pid`的方式跟踪子进程，其中`pid`为子进程的进程ID
	  2. 在`gdb`中使用`set follow-fork-mode`配置`fork`时跟踪子进程还是父进程
   
	  参考资料：
	  - [gdb面试](https://blog.csdn.net/cindywry/article/details/105436462)
	  - [Debugging programs with multiple processes](https://ftp.gnu.org/old-gnu/Manuals/gdb/html_node/gdb_25.html)
    </details>

5. 如何调试`多线程`程序？

	<details>
      <summary>参考答案</summary>

      参考资料：
	  - [Debugging programs with multiple threads](https://ftp.gnu.org/old-gnu/Manuals/gdb/html_node/gdb_24.html#SEC25)
    </details>

6. 什么是`core`文件？有什么作用？

	<details>
      <summary>参考答案</summary>

    </details>