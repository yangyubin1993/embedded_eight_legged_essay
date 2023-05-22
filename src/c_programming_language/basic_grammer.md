C语言基础语法知识
===

1. C语言有哪些`存储类型(Storage Class)`?
   <details>
      <summary>参考答案</summary>
    
      存储类型主要定义程序对象（变量及函数）的存储生命周期及作用域；C语言的四种存储类型及其生命周期和作用域分别为：

      ![c_storage_class](https://yangpaopao.space/wp-content/uploads/2023/05/2541684493282_.pic_.jpg)

      `register`修饰符有特殊的限制，具体如下：
      ```
      objects declared with the register storage class may be given higher priority by the compiler for access to registers; although the compiler may choose not to actually store any of them in a register. Objects with this storage class may not be used with the address-of (&) unary operator.
      ```
      即使用`register`修饰的变量，会优先存储在CPU寄存器中（但不一定会存储在寄存器中，因为寄存器数量是有限的），而且该变量不能使用取地址符(&);

      参考资料：
      - [Storage class specifiers](https://en.wikipedia.org/wiki/C_syntax#Storage_class_specifiers)
    </details>

2. C语言中`static`关键字有哪些作用？
    <details>
      <summary>参考答案</summary>
    
      `static`修饰符可用于修饰全局变量、局部变量或函数，三种场景下的作用分别为：
      1. 修饰全局变量时：被修饰的变量称为静态全局变量。该全局变量仅在当前文件内可见。
      2. 修饰局部变量时：被修饰的变量称为静态局部变量。变量仅初始化一次，而且由于变量是存储在数据段，而非堆或栈上，因此局部变量在离开作用域后不会被销毁，变量值始终有效直至程序结束。
      3. 修饰函数时：被修饰的函数称为静态函数。该函数仅在当前文件内可见。

      参考资料：
      - [wikipedia static keyword](https://en.wikipedia.org/wiki/Static_(keyword))
      - [C程序的内存分配](about_compile.md#memory_layout_of_c)
    </details>

3. 是否可以在头文件中定义`static`变量？
    <details>
      <summary>参考答案</summary>
    
      可以，但包含该头文件的源文件会有命名相同但实际不同的`static`变量。

      参考资料:
      - [Is it possible to declare a static variable in a header file?](https://www.interviewbit.com/embedded-c-interview-questions/#is-it-possible-to-declare-static-variable-in-header-file)
    </details>
  
4. `volatile`的作用是什么，什么时候需要使用`volatile`？
    <details>
      <summary>参考答案</summary>

      `volatile`修饰变量时表示变量的值可能有多个途径进行修改，尽管在代码上并没有显式修改变量值。因此`volatile`用于指示编译器针对所修饰的变量不要进行编译优化，防止编译器优化导致变量值的读写异常。

      举个简单的例子，以下代码中全局静态变量`b`不使用`volatile`修饰：
      ```c
      static int b;
      int main() {
          b = 1;
          while (b != 255) {
              ;
          }
          return 0;
      }
      ```

      其生成的二进制如下(使用gcc -O3)：

      ```
      Disassembly of section __TEXT,__text:

      0000000000000000 <_main>:
             0: 55                           	pushq	%rbp
             1: 48 89 e5                     	movq	%rsp, %rbp
             4: 66 2e 0f 1f 84 00 00 00 00 00	nopw	%cs:(%rax,%rax)
             e: 66 90                        	nop
            10: eb fe                        	jmp	0x10 <_main+0x10>
      ```

      而加上`volatile`修饰之后的，其二进制如下：

      ```
      Disassembly of section __TEXT,__text:

      0000000000000000 <_main>:
             0: 55                           	pushq	%rbp
             1: 48 89 e5                     	movq	%rsp, %rbp
             4: c7 05 fc ff ff ff 01 00 00 00	movl	$1, -4(%rip)            ## 0xa <_main+0xa>
             e: 66 90                        	nop
            10: 8b 05 00 00 00 00            	movl	(%rip), %eax            ## 0x16 <_main+0x16>
            16: 3d ff 00 00 00               	cmpl	$255, %eax
            1b: 75 f3                        	jne	0x10 <_main+0x10>
            1d: 31 c0                        	xorl	%eax, %eax
            1f: 5d                           	popq	%rbp
            20: c3                           	retq
      ```
      从生成的不同的二进制我们可以看到，不加`volatile`修饰时，并没有比较`b`和`255`的值，即代码优化导致实际的代码逻辑出现异常。

      参考资料：
      - [volatile (computer programming)](https://en.wikipedia.org/wiki/Volatile_(computer_programming))
      - [Why do we use the volatile keyword?](https://www.interviewbit.com/embedded-c-interview-questions/#why-do-we-use-volatile-keyword)
  
    </details>

5. `inline`和`macro`在使用上有什么区别？
    <details>
      <summary>参考答案</summary>

      `inline`和`macro`均可以用于做代码的替换，这两者的差别主要有：
      1. 代码展开的阶段不同。`macro`在预处理阶段就进行展开，而`inline`在代码编译过程展开。
      2. 类型检查的要求不同。`macro`并不做类型检查，而`inline`函数本身就是函数，会做类型检查。
      3. 表达式计算的方式不同。`macro`可能会对表达式进行多次运算，而`inline`函数仅在表达式传入函数时进行运算。如`#define sum(a, b) (a) + (b)`和`inline func(int a, int b) { return a + b; }`分别使用`sum(a++)`和`func(a++, b)`进行调用时，前者`a++`计算了两次，而后者`a++`仅计算一次。

      针对`inline`需要注意的是：
      1. `inline`只是建议编译器对函数进行内联展开，编译器并不一定会采纳。
      2. 在支持热补丁的场景下，采用`inline`可能是一个bad idea。

      参考资料：
      - [What are the differences between Inline and Macro Function?](https://www.interviewbit.com/embedded-c-interview-questions/#differences-between-inline-and-macro-function)
      - [Comparison with macros](https://en.wikipedia.org/wiki/Inline_expansion#Comparison_with_macros)
    </details>

6. 什么是`Segmentation Fault`，什么时候会出现，如何避免？
    <details>
      <summary>参考答案</summary>
    
      `Segmentation Fault`中文译为`段错误`，出现段错误主要是因为程序访问到无权限访问的内存区域。常见的段错误场景主要有：
      1. 对空指针(NULL/nullptr)或未初始化的指针（指针可能指向无效地址）进行解引用(dereference)
      2. 数组越界访问
      3. 对只读区域的内存进行更新或访问无效/无权限的内存区域（如内核态地址空间）

      避免段错误可以考虑使用静态代码扫描工具，如PC-lint等，扫描代码是否存在以下问题：
      1. 指针变量未初始化
      2. 数组是否可能存在越界访问

      参考资料：
      - [What are the reasons for segmentation fault in Embedded C? How do you avoid these errors?](https://www.interviewbit.com/embedded-c-interview-questions/#reasons-for-segmentation-fault-to-occur-how-to-avoid-it)
    </details>