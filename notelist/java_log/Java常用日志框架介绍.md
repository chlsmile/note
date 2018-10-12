# Java常用日志框架介绍
## java日志概述
> 对于一个应用程序来说日志记录是必不可少的一部分。线上问题追踪，基于日志的业务逻辑统计分析等都离不日志。java领域存在多种日志框架，目前常用的日志框架包括Log4j，Log4j 2，Commons Logging，Slf4j，Logback，Jul。

##java常用日志框架类别介绍
* **Log4j** Apache Log4j是一个基于Java的日志记录工具。它是由Ceki Gülcü首创的，现在则是Apache软件基金会的一个项目。 Log4j是几种Java日志框架之一。

* **Log4j 2** Apache Log4j 2是apache开发的一款Log4j的升级产品。

* **Commons Logging** Apache基金会所属的项目，是一套Java日志接口，之前叫Jakarta Commons Logging，后更名为Commons Logging。

* **Slf4j** 类似于Commons Logging，是一套简易Java日志门面，本身并无日志的实现。（Simple Logging Facade for Java，缩写Slf4j）。

* **Logback** 一套日志组件的实现(slf4j阵营)。

* **Jul** (Java Util Logging),自Java1.4以来的官方日志实现。

看了上面的介绍是否会觉得比较混乱，这些日志框架之间有什么异同，都是由谁在维护? 下文会逐一介绍。

 
## Java常用日志框架历史
* 1996年早期，欧洲安全电子市场项目组决定编写它自己的程序跟踪API(Tracing API)。经过不断的完善，这个API终于成为一个十分受欢迎的Java日志软件包，即Log4j。后来Log4j成为Apache基金会项目中的一员。

* 期间Log4j近乎成了Java社区的日志标准。据说Apache基金会还曾经建议sun引入Log4j到java的标准库中，但Sun拒绝了。

* 2002年Java1.4发布，Sun推出了自己的日志库JUL(Java Util Logging),其实现基本模仿了Log4j的实现。在JUL出来以前，log4j就已经成为一项成熟的技术，使得log4j在选择上占据了一定的优势。

* 接着，Apache推出了Jakarta Commons Logging，JCL只是定义了一套日志接口(其内部也提供一个Simple Log的简单实现)，支持运行时动态加载日志组件的实现，也就是说，在你应用代码里，只需调用Commons Logging的接口，底层实现可以是log4j，也可以是Java Util Logging。

* 后来(2006年)，Ceki Gülcü不适应Apache的工作方式，离开了Apache。然后先后创建了slf4j(日志门面接口，类似于Commons Logging)和Logback(Slf4j的实现)两个项目，并回瑞典创建了QOS公司，QOS官网上是这样描述Logback的：The Generic，Reliable Fast&Flexible Logging Framework(一个通用，可靠，快速且灵活的日志框架)。

* 现今，Java日志领域被划分为两大阵营：Commons Logging阵营和SLF4J阵营。
Commons Logging在Apache大树的笼罩下，有很大的用户基数。但有证据表明，形式正在发生变化。2013年底有人分析了GitHub上30000个项目，统计出了最流行的100个Libraries，可以看出slf4j的发展趋势更好：

![pic1](https://github.com/chlsmile/note/blob/master/notefile/log/java_populor_jar.png)
 
* Apache眼看有被Logback反超的势头，于2012-07重写了log4j 1.x，成立了新的项目Log4j 2。Log4j 2具有logback的所有特性。

##java常用日志框架之间的关系
* Log4j2与Log4j1发生了很大的变化，log4j2不兼容log4j1。

* Commons Logging和Slf4j是日志门面(门面模式是软件工程中常用的一种软件设计模式，也被称为正面模式、外观模式。它为子系统中的一组接口提供一个统一的高层接口，使得子系统更容易使用)。log4j和Logback则是具体的日志实现方案。可以简单的理解为接口与接口的实现，调用这只需要关注接口而无需关注具体的实现，做到解耦。

* 比较常用的组合使用方式是Slf4j与Logback组合使用，Commons Logging与Log4j组合使用。

* Logback必须配合Slf4j使用。由于Logback和Slf4j是同一个作者，其兼容性不言而喻。

##Commons Logging与Slf4j实现机制对比

###### Commons logging实现机制  
Commons logging是通过动态查找机制，在程序运行时，使用自己的ClassLoader寻找和载入本地具体的实现。详细策略可以查看commons-logging-*.jar包中的org.apache.commons.logging.impl.LogFactoryImpl.java文件。由于OSGi不同的插件使用独立的ClassLoader，OSGI的这种机制保证了插件互相独立, 其机制限制了commons logging在OSGi中的正常使用。

###### Slf4j实现机制
Slf4j在编译期间，静态绑定本地的LOG库，因此可以在OSGi中正常使用。它是通过查找类路径下org.slf4j.impl.StaticLoggerBinder，然后绑定工作都在这类里面进。
 

## 如果在项目中如果选择日志框架
如果是在一个新的项目中建议使用Slf4j与Logback组合，这样有如下的几个优点。

1. Slf4j实现机制决定Slf4j限制较少，使用范围更广。由于Slf4j在编译期间，静态绑定本地的LOG库使得通用性要比Commons logging要好。

2. Logback拥有更好的性能。Logback声称：某些关键操作，比如判定是否记录一条日志语句的操作，其性能得到了显著的提高。这个操作在Logback中需要3纳秒，而在Log4J中则需要30纳秒。LogBack创建记录器（logger）的速度也更快：13毫秒，而在Log4J中需要23毫秒。更重要的是，它获取已存在的记录器只需94纳秒，而Log4J需要2234纳秒，时间减少到了1/23。跟JUL相比的性能提高也是显著的。

3. Commons Logging开销更高 在使Commons Logging时为了减少构建日志信息的开销，通常的做法是：
if(log.isDebugEnabled()){
  log.debug("User name： " +
    user.getName() + " buy goods id ：" + good.getId());
}
在Slf4j阵营，你只需这么做：
log.debug("User name：{} ,buy goods id ：{}", user.getName(),good.getId());
也就是说，slf4j把构建日志的开销放在了它确认需要显示这条日志之后，减少内存和cup的开销，使用占位符号，代码也更为简洁

4. Logback文档免费。Logback的所有文档是全面免费提供的，不象Log4J那样只提供部分免费文档而需要用户去购买付费文档。

## 如何在项目中使用Slf4j
#### Slf4j与其他各种日志组件的桥接

| jar包名 | 说明 |
| :------------ |:------------- |
|**slf4j-log4j12-1.7.13.jar** | log4j1.2版本的桥接器，你需要将log4j.jar加入classpath。| 
| **slf4j-jdk14-1.7.13.jar** | java.util.logging的桥接器，JDK原生日志框架。|
| **slf4j-nop-1.7.13.jar** | NOP桥接器，默默丢弃一切日志。|
| **slf4j-simple-1.7.13.jar** |一个简单实现的桥接器，该实现输出所有事件到System.err. 只有INFO以及高于该级别的消息被打印，在小型应用中它也许是有用的。|
|**slf4j-jcl-1.7.13.jar**|Jakarta Commons Logging 的桥接器. 这个桥接器将SLF4j所有日志委派给JCL。|
|**logback-classic-1.0.13.jar(requires logback-core-1.0.13.jar)**|slf4j的原生实现，logback直接实现了slf4j的接口，因此使用slf4j与 logback的结合使用也意味更小的内存与计算开销|

具体的接入方式参见下图
 ![pic2](https://github.com/chlsmile/note/blob/master/notefile/log/slf4j-concrete-bindings1.png)

#### 如何桥接遗留的api
在实际环境中我们经常会遇到不同的组件使用的日志框架不同的情况，例如Spring Framework使用的是日志组件是Commons logging，XSocket依赖的则是Java Util Logging。当我们在同一项目中使用不同的组件时应该如果解决不同组件依赖的日志组件不一致的情况呢？现在我们需要统一日志方案，统一使用SLF4J，把他们的日志输出重定向到SLF4J，然后 SLF4J 又会根据绑定器把日志交给具体的日志实现工具。Slf4j带有几个桥接模块，可以重定向log4j，JCL和java.util.logging中的API到Slf4j。

遗留的api桥接方案

jar包名 | 作用|
:----------- | :-----------| 
**log4j-over-slf4j-version.jar**| 将log4j重定向到slf4j|
**jcl-over-slf4j-version.jar**|将commos logging里的Simple Logger重定向到slf4j|
**jul-to-slf4j-version.jar** |将Java Util Logging重定向到slf4j|

桥接方式参见下图
 ![pic3](https://github.com/chlsmile/note/blob/master/notefile/log/slf4j_brige.png)
 
使用slf4j桥接要注意事项

在使用slf4j桥接时要注意避免形成死循环，在项目依赖的jar包中不要存在以下情况。

多个日志jar包形成死循环的条件| 产生原因|
:-----------|:-----------| 
**log4j-over-slf4j.jar和slf4j-log4j12.jar同时存在**|由于slf4j-log4j12.jar的存在会将所有日志调用委托给log4j。但由于同时由于log4j-over-slf4j.jar的存在，会将所有对log4j api的调用委托给相应等值的slf4j,所以log4j-over-slf4j.jar和slf4j-log4j12.jar同时存在会形成死循环|
**jul-to-slf4j.jar和slf4j-jdk14.jar同时存在**|由于slf4j-jdk14.jar的存在会将所有日志调用委托给jdk的log。但由于同时jul-to-slf4j.jar的存在，会将所有对jul api的调用委托给相应等值的slf4j，所以jul-to-slf4j.jar和slf4j-jdk14.jar同时存在会形成死循环|

## 参考链接

[slf4j官网](http://www.slf4j.org)

[slf4j使用手册1](http://www.slf4j.org/manual.html)

[slf4j使用手册2](http://www.slf4j.org/legacy.html)

[logback官网](http://logback.qos.ch)

[commons logging官网](https://commons.apache.org/proper/commons-logging)


 
 
 
 




 





 
 
 





