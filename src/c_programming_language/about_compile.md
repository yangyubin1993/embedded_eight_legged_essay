C语言编译相关知识
===

1. <a name="memory_layout_of_c"></a>C程序的内存分配
    <details>
      <summary>参考答案</summary>
    
    C程序内存分配为以下五个区：
    1. text (或code): 存储可执行代码，通常是固定大小而且是只读的。
    2. data： 存储`已初始化`的全局变量或静态局部变量。
    3. bss(Block Started by Symbol): 存储`未初始化`的全局变量或静态局部变量。
    4. heap: 存储动态分配的内存段，一般从bss尾部往高地址内存区增长。
    5. stack: 用于调用栈，从高地址内存区往低地址内存区增长。
   
    五个区的分布图可参考：

    ![program memory layout](https://upload.wikimedia.org/wikipedia/commons/thumb/5/50/Program_memory_layout.pdf/page1-94px-Program_memory_layout.pdf.jpg)

    在上面的五个区中可以发现，`bss`区和`data`区都是用于存储全局变量值或静态局部变量值的，只是前者是存储未初始化的，而后者是存储已初始化的。我们知道C语言中，未定义的`static`变量一般都会默认初始化为0，那么为什么还要拆成两个区来存储？
    
    其实之所以拆成`bss`区和`data`区主要是为了减小程序大小。因为`data`区和`bss`区有如下的处理差异：
    - text 和 data 段都在可执行文件中，由系统从可执行文件中加载
    - bss 段不在可执行文件中，由系统初始化。
  
    即如果我们将无需初始化的变量放在bss区，bss区只存储标识符，那么只需要在程序启动时将需要初始化为0的未初始化变量初始化为0即可。这样可以减少程序大小，从而降低ROM空间的开销（在嵌入式设备上，采用更低规格的ROM可以降低成本）。

    另外还需要注意的是，将程序划分为以上五个区只是典型的情况，不同的操作系统可能会有不同的实现。
    参考资料：
    - [Program Memory](https://en.wikipedia.org/wiki/Data_segment#Program_memory)
    - [.bss](https://en.wikipedia.org/wiki/.bss)
    - [Why is the .bss segment required?](https://stackoverflow.com/questions/9535250/why-is-the-bss-segment-required)
    - [深入理解BSS段与data段的区别](https://www.jianshu.com/p/ddfb284c1f7a)
    </details>

2. gcc的编译有哪几个过程，每个过程的作用是什么？
    <details>
      <summary>参考答案</summary>

      gcc编译分为四个过程：预处理、编译、汇编、链接。四个过程的作用分别如下：

      1. 预处理(c pre-processing)：C Pre-processing简写为`cpp`，在gcc编译过程中主要由`cpp`程序负责该过程的代码处理。该过程主要做一些文本的初始化处理(如移除注释)、源文件所需头文件(`#include`)内容拷贝到源文件中及将`macro`进行展开。预处理完后会生成`*.i`文件，是一下过程`编译`的的输入。在gcc上，可以使用如下命令对文件进行预处理：
   
      ```shell
      gcc -E input.c -o input.i
      ```

      2. 编译(Compilation): 编译过程将前一过程生成的`*.i`文件进行编译以生成特定架构上的汇编代码。生成的汇编代码文件以`s`作为文件名后缀。在gcc上，可以使用如下命令生成文件的汇编代码：
      
      ```shell
      gcc -S input.i
      ```
   
      3. 汇编(Assembly)：汇编过程将汇编代码转化为机器代码（即二进制文件），生成的文件以`o`为文件名后缀。在gcc套件中，汇编过程是由`as`程序负责的，可以使用如下命令生成文件的机器代码：
   
      ```shell
      gcc -c input.s
      ```

      4. 链接(Linker): 链接过程将生成的二进制文件与依赖的库文件进行链接从而生成可执行文件。链接过程由程序`ld`负责。
   
      参考资料：
      - [Options Controlling the Kind of Output](https://gcc.gnu.org/onlinedocs/gcc/Overall-Options.html)
      - [GCC Compilation Process](https://www3.ntu.edu.sg/home/ehchua/programming/cpp/gcc_make.html)
    </details>

3. make的作用？

    <details>
      <summary>参考答案</summary>

      make是软件开发过程中非常常用的一个工具，它读取工程中的`makefile`文件以自动构建软件。`makefile`文件主要格式为：`目标` + `依赖` + `规则`，如下：

      ```makefile
      target: dependencies
      <TAB>command-1
      <TAB>command-2
      ```

      参考资料：
      - [wikipedia: make](https://zh.wikipedia.org/zh-cn/Make)
    </details>

4. CMake的作用？

    <details>
      <summary>参考答案</summary>

      CMake是一个跨平台的、开源的自动化建构系统，用于软件的自动构建、测试、打包和安装。CMake本身并不具备构建功能，而是通过读取`CMakeList.txt`生成其它构建系统的构建文件（如生成`make`系统的`makefile`、生成`Windows MSVC`的`projects/workspaces`）。再通过这些生成的构建文件去做软件的构建。
      对C/C++程序来说，CMake的优点主要有：
      1. 支持跨平台，如Linux和Windows
      2. 脚本`较`makefile简单易读
   
      CMake的缺点也很明显：强大但也很复杂，调试麻烦，对开发人员要求较高。

      参考资料：
      - [wikipedia: CMake](https://en.wikipedia.org/wiki/CMake)
    </details>

5. 解释编译器的前端和后端的区别。
   <details>
      <summary>参考答案</summary>

    </details>
6. 什么是交叉编译？为什么在嵌入式开发中需要使用交叉编译器？
   <details>
      <summary>参考答案</summary>

    </details>
7. 什么是链接器？它的作用是什么？解释静态链接和动态链接的区别
   <details>
      <summary>参考答案</summary>

    </details>
8. 什么是库文件（Library）？解释静态库和动态库的区别，并讨论它们在嵌入式开发中的使用场景。
   <details>
      <summary>参考答案</summary>

    </details>
9.  请讨论一些常见的编译器选项和优化策略，以优化嵌入式软件的性能和大小。
    <details>
      <summary>参考答案</summary>

    </details>
10. 解释编译器标志（Compiler Flag）-nostdlib的作用，并讨论在嵌入式开发中使用它的情况。
    <details>
      <summary>参考答案</summary>

    </details>
11. 什么是目标文件和可执行文件？它们的区别是什么？
    <details>
      <summary>参考答案</summary>

    </details>
12. 什么是交叉引用（Cross-Reference）？如何生成交叉引用报告？
    <details>
      <summary>参考答案</summary>

    </details>
13. 解释链接时的符号解析过程是什么？包括全局符号和局部符号的解析。
    <details>
      <summary>参考答案</summary>

    </details>
14. 什么是位置无关代码（Position-Independent Code，PIC）？它在嵌入式系统中的作用是什么？
    <details>
      <summary>参考答案</summary>

    </details>