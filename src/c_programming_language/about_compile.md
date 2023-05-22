C语言编译相关知识
===

1. <a name="memory_layout_of_c"></a>C程序的内存分配
    <details>
      <summary>参考答案</summary>
    
    C程序内存分配为五个区：
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

    参考资料：
    - [Program Memory](https://en.wikipedia.org/wiki/Data_segment#Program_memory)
    - [.bss](https://en.wikipedia.org/wiki/.bss)
    - [Why is the .bss segment required?](https://stackoverflow.com/questions/9535250/why-is-the-bss-segment-required)
    - [深入理解BSS段与data段的区别](https://www.jianshu.com/p/ddfb284c1f7a)
    </details>