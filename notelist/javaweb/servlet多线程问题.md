## servlet多线程问题

### servlet默认是线程不安全的

- Servlet容器可以并发的发送多个请求到Servlet的service方法。为了处理这些请求，Servlet开发者必须为service方法的多线程并发处理做好充足的准备。一个替代的方案是开发人员实现SingleThreadModel接口，由容器保证一个service方法在同一个时间点仅被一个请求线程调用，但是此方案是不推荐的。Servlet容器可以通过串行化访问Servlet的请求，或者维护一个Servlet实例池完成该需求。如果Web 应用中的Servlet被标注为分布式的，容器应该为每一个分布式应用程序的JVM维护一个Servlet实例池。

- 对于那些没有实现SingleThreadModel 接口的Servlet，但是它的service方法(或者是那些HttpServlet 中通过service 方法分派的doGet、doPost 等分派方法)是通过synchronized 关键词定义的，Servlet容器不能使用实例池方案，并且只能使用序列化请求进行处理。强烈推荐开发人员不要去通过service方法（或者那些由Service 分派的方法），因为这将严重影响性能。

### servlet多线程注意事项

- 当Server Thread线程执行Servlet实例的init()方法时，所有的Client Service Thread线程都不能执行该实例的service()方法，更没有线程能够执行该实例的destroy()方法，因此Servlet的init()方法是工作在单线程的环境下，开发者不必考虑任何线程安全的问题。

- 当服务器接收到来自客户端的多个请求时，服务器会在单独的Client Service Thread线程中执行Servlet实例的service()方法服务于每个客户端。此时会有多个线程同时执行同一个Servlet实例的service()方法，因此必须考虑线程安全的问题。

- 虽然service()方法运行在多线程的环境下，并不一定要同步该方法。而是要看这个方法在执行过程中访问的资源类型及对资源的访问方式。

> 如果service()方法没有访问Servlet的成员变量也没有访问全局的资源比如静态变量、文件、数据库连接等，而是只使用了当前线程自己的资源，比如非指向全局资源的临时变量、request和response对象等。该方法本身就是线程安全的，不必进行任何的同步控制。
> 如果service()方法访问了Servlet的成员变量，但是对该变量的操作是只读操作，该方法本身就是线程安全的，不必进行任何的同步控制。
> 如果service()方法访问了Servlet的成员变量，并且对该变量的操作既有读又有写，通常需要加上同步控制语句。
> 如果service()方法访问了全局的静态变量，如果同一时刻系统中也可能有其它线程访问该静态变量，如果既有读也有写的操作，通常需要加上同步控制语句。
> 如果service()方法访问了全局的资源，比如文件、数据库连接等，通常需要加上同步控制语句。