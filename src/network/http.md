http协议相关知识
===

1. http和https有什么区别？
   
	<details>
      <summary>参考答案（答案来源于ChatGpt）</summary>

      HTTP（Hypertext Transfer Protocol）和HTTPS（Hypertext Transfer Protocol Secure）是用于在客户端和服务器之间传输数据的两种协议。它们的主要区别在于安全性和加密方面：

      1. `安全性`：HTTP是一种不安全的协议，数据在传输过程中以明文形式传输，容易被攻击者窃听、篡改或伪装。而HTTPS通过使用TLS（Transport Layer Security）或SSL（Secure Sockets Layer）协议对数据进行加密和认证，提供了更高的安全性和保密性。

      2. `加密通信`：HTTP不提供数据的加密传输，使得敏感信息（如登录凭据、信用卡号等）容易被攻击者获取。而HTTPS使用SSL/TLS协议对通信进行加密，确保数据在传输过程中的机密性，使得攻击者无法轻易获取敏感信息。

      3. `证书验证`：HTTPS使用SSL/TLS证书对服务器进行身份验证，确保客户端与服务器之间的通信建立在可信任的连接上。客户端会验证服务器的证书，以确保与合法和受信任的服务器建立连接。这样可以防止中间人攻击和DNS劫持等安全威胁。

      4. `默认端口`：HTTP使用端口号80进行通信，而HTTPS使用端口号443进行加密通信。

      HTTPS在保护用户隐私和数据安全方面比HTTP更加可靠，因此在需要保护敏感信息的场景，如电子商务网站、在线支付平台等，推荐使用HTTPS。

      参考资料：
      - [MDN Web Docs: HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
      - [MDN Web Docs: HTTPS](https://developer.mozilla.org/en-US/docs/Web/HTTP/HTTPS)
      - [Difference Between HTTP and HTTPS](https://www.cloudflare.com/learning/ssl/why-use-https/)
      - [HTTP vs HTTPS: What's the Difference and Why Should You Care?](https://www.cloudflare.com/learning/ssl/http-vs-https/)
      - [HTTP vs HTTPS: The Difference Between SSL and TLS](https://www.cloudflare.com/learning/ssl/ssl-vs-tls/)
    </details>