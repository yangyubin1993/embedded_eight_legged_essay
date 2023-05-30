TCP && UDP基础知识
===

1. tcp和udp有什么区别？一般用于哪些场景？
   
	<details>
      <summary>参考答案（答案来源于ChatGpt）</summary>

      TCP（Transmission Control Protocol）和UDP（User Datagram Protocol）是两种常见的传输层协议，它们有以下区别：

      1. `可靠性`：TCP提供可靠的数据传输，确保数据的完整性和顺序性。它使用确认机制、重传机制和流量控制来处理丢失、重复、损坏和失序的数据。而UDP是无连接的、不可靠的协议，它不提供数据的可靠性保证，数据包可能会丢失或以乱序的方式到达。

      2. `速度和效率`：由于TCP提供可靠性保证，它的传输速度较慢。TCP维护连接状态信息、进行确认和重传，这些额外的开销会带来一定的延迟和网络开销。相比之下，UDP没有这些额外的开销，传输速度更快，延迟更低。

      3. `连接性`：TCP是面向连接的协议，通信双方在传输数据之前需要先建立连接，然后进行数据传输，最后再关闭连接。UDP是无连接的协议，发送方可以直接发送数据包给接收方，无需建立连接。

      4. `数据包大小`：TCP没有数据包大小限制，可以传输较大的数据。UDP的数据包大小受限制，每个数据包的最大长度为64KB，如果超过这个限制，数据将被分片或被丢弃。

      5. `适用场景`：TCP适用于对数据完整性和顺序性要求较高的场景，如网页浏览、文件传输、电子邮件等。UDP适用于实时性要求高、数据丢失不重要的场景，如实时音视频传输、在线游戏、DNS查询等。

      总的来说，TCP提供可靠的、有序的数据传输，适用于对数据完整性要求高的场景。而UDP提供快速的、无连接的数据传输，适用于实时性要求高、对数据可靠性要求较低的场景。

      需要根据具体应用需求和场景来选择使用TCP还是UDP。有些应用可能同时使用两种协议，如视频会议应用可以使用UDP传输实时音视频数据，同时使用TCP传输控制和数据确认信息。

      参考资料：
      - [TCP vs UDP: What's the Difference? (Cloudflare)](https://www.cloudflare.com/learning/ddos/glossary/tcp-vs-udp/)
      - [TCP vs UDP: What is the Difference between TCP and UDP? (GeeksforGeeks)](https://www.geeksforgeeks.org/tcp-vs-udp-proto/)
      - [TCP/IP Guide: TCP and UDP Transport Layer Protocols (TCP/IP Guide)](https://www.tcpipguide.com/free/t_TCPIPTCPandUDPTransportLayerProtocols.htm)
      - [TCP vs. UDP: Differences You Need to Know (KeyCDN)](https://www.keycdn.com/support/tcp-vs-udp)
      - [TCP/IP: TCP vs UDP (NetworkLessons)](https://networklessons.com/cisco/ccna-routing-switching-icnd1-100-105/tcpip-tcp-vs-udp)
    </details>