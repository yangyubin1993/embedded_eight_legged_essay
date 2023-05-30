计算机网络基础知识
===

1. OSI七层模型是怎样的？每层的作用是什么？

 	<details>
      <summary>参考答案</summary>

      OSI七层模型是`ISO`组织提出的，试图使各种计算机在世界范围内互连为网络的标准框架。OSI模型并没有提供实现的方法，仅提供一个概念框架，共分为七层，从低到上分别为：

      1. `物理层(Physical Layer)`: 负责在不同的物理设备之间传递和接收比特流，该层会将数字信号转移为电信号或光信号等。支持的协议包含Ethernet、WiFi等
      2. `数据链路层(Data link Layer)`: 在由物理层连接的两个节点间传输数据帧(Data Frames)，实现可靠的数据传输。支持的协议包含Ethernet、WiFi、PPP等
      3. `网络层(Network Layer)`: 处理数据包在网络中的路由和转发。支持的协议包含IP、ICMP、ARP等
      4. `传输层(Transport layer)`: 提供可靠的端到端数据传输。支持的协议包含TCP、UDP等
      5. `会话层(Session Layer)`: 建立、管理和终止会话。支持的协议包含RPC等
      6. `表示层(Presentation Layer)`: 实现数据格式的转换、加密和压缩。支持的协议包含SSL等
      7. `应用层(Application Layer)`: 提供应用程序之间的通信。支持的协议包含SSH、HTTP等

      参考资料:
      - [中文维基百科:OSI模型](https://zh.wikipedia.org/wiki/OSI模型)
      - [英文维基百科:OSI模型](https://en.wikipedia.org/wiki/OSI_model)

    </details>

2. TCP/IP四层模型是怎样的？每层的作用是什么？

	<details>
      <summary>参考答案（答案来源于ChatGpt）</summary>

      TCP/IP模型是一个常用的网络协议栈，它包含四个层次，每个层次都有特定的功能和作用。以下是TCP/IP模型的各层次及其作用：
      1. `网络接口层（Network Interface Layer）`：
         - __作用__：提供物理网络和数据链路层之间的接口，处理数据帧的发送和接收，以及物理地址（MAC地址）的解析和处理。
         - __协议__：Ethernet、Wi-Fi、PPP（点对点协议）等。
      2. `网络层（Internet Layer）`：
         - __作用__：处理数据包的路由和转发，实现不同网络之间的数据通信，以及网络寻址和逻辑地址（IP地址）的管理。
         - __协议__：IP（Internet Protocol）、ICMP（Internet Control Message Protocol）、ARP（Address Resolution Protocol）等。
      3. `传输层（Transport Layer）`：
         - __作用__：提供端到端的可靠数据传输服务，确保数据的可靠性和完整性，并处理多个应用程序之间的数据传输。
         - __协议__：TCP（Transmission Control Protocol）、UDP（User Datagram Protocol）等。
      4. `应用层（Application Layer）`：
         - __作用__：支持特定的网络应用程序，提供各种应用层协议和服务，使应用程序能够进行数据交换和通信。
         - __协议__：HTTP（Hypertext Transfer Protocol）、FTP（File Transfer Protocol）、SMTP（Simple Mail Transfer Protocol）、DNS（Domain Name System）等。
  
      需要注意的是，TCP/IP模型中的层次与OSI七层模型不完全对应。网络接口层对应了OSI模型的物理层和数据链路层，而网络层在一定程度上涵盖了OSI模型的网络层功能，传输层和应用层则在OSI模型的传输层和应用层上进行了合并和扩展。

      TCP/IP模型是互联网的基础协议栈，它定义了一组协议和规范，使得不同计算机和网络设备能够进行互联并进行数据通信
  </details>