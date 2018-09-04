## servlet与servlet容器

#### 什么是servlet
- Servlet是基于Java技术的web组件，容器托管的，用于生成动态内容。
  像其他基于Java的组件技术一样，Servlet也是基于平台无关的Java类格式，被编译为平台无关的字节码，可以被基于Java技术的web server动态加载并运行。
  容器，有时候也叫做servlet引擎，是web server 为支持servlet功能扩展的部分。客户端通过Servlet容器实现的请求/应答模型与Servlet交互。



#### 什么是servlet容器
- Servlet容器是web server 或application server的一部分，提供基于请求/响应发送模型的网络服务，解码基于MIME的请求，并且格式化基于MIME的响应。Servlet 容器也包含了管理Servlet生命周期。

- 所有Servlet容器必须支持基于HTTP协议的请求/响应模型，比如像基于HTTPS（HTTP over SSL）协议的请求/应答模型可以选择性的支持。容器必须实现的HTTP协议版本包含HTTP/1.0和HTTP/1.1。


