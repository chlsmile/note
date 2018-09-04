# 理解Java类加载机制(译文)

## 理解java类加载机制

> 你想写类加载器？或者你遇到了ClassCastException异常，或者你遇到了奇怪的LinkageError状态约束异常。应该仔细看看java类的加载处理了。

## 什么是类加载器以及它是如何对类进行加载的?


一个Java类是由**java.lang.ClassLoader**类的一个实例加载的。由于java.lang.ClassLoader自己本身是一个抽象类所以一个类加载器只能够是java.lang.ClassLoader类的具体子类的实例。如果是这种情况,那么哪一个类加载器来加载java.lang.ClassLoader这个类？(经典的"谁将会加载加载者"引导的问题)。事实证明JVM有一个内置的引导类加载器。引导加载器加载java.lang.ClassLoader和许多其他java平台类。


要加载一个具体的java类，例如com.acme.Foo，JVM调用java.lang.ClassLoader类的loadClass方法(事实上，JVM查找loadClassInternal方法-如果发现loadClassInternal方法则用loadClassInternal方法，否则JVM使用loadClass方法，而loadClassInternal方法会调用loadClass方法)。loadClass方法接收类名来加载类返回表示加载的类的java.lang.Class实例。事实上loadClass方法找到.class文件(或者URL)的实际字节，并调用defineClass方法来构造出java.lang.Class类的字节数组。加载器上调用loadClass方法的加载器称之为初始化加载器(即，JVM启动加载使用这个加载器).但是，启动加载器不是直接加载类的-而是可能委托给另外一个类加载器(例如，它的父加载器)-它自己也可能委派给另外一个加载器去加载等等。最终在委托链中的某些类加载器对象调用defineClass方法加载有关的类(com.acme.Foo)。
这个特殊的类加载器叫做com.acme.Foo的确切加载器。在运行时，一个java类是由类的完全限定类名和和类加载器确定其唯一性的。如果指定相同的类名(即,相同的完全限定类名)的类是由两个不同的类加载器加载的,那么这些类是不同的-即使这些.class的字节码是相同的并且都是从相同的位置进行加载的(相同的URL)。

## 有多少种类加载器并且它们是从哪里加载类的?

即便是一个简单的"hell world"java程序，也有至少3种类加载器。

1. 引导类加载器

	* 加载java平台基础类(例如java.lang.Object，java.lang.Thread等)。
	* 加载rt.jar包种的类($JRE_HOME/lib/rt.jar)。
	* -Xbootclasspath参数可以更改启动类路径-Xbootclasspath/p: 和 -Xbootclasspath/a:参数可以前置/追加额外的引导目录-一定要格外小心这样做。在大多数情况下，要避免随意变更启动类路径。
	* 在Sun的实现中，只读系统属性sun.boot.class.path设置为指向启动类路径。注意你不能在运行时修改这个属性-如果你修改了修改也不会生效。
	* 这个加载器由java的null表示。例如，java.lang.Object.class.getClassLoader()方法将会返回null(还有其他的类例如java.lang.Integer，java.awt.Frame，java.sql.DriverManager等)


2. 扩展类加载器
	* 从已安装的可选包中加载类。
	* 从$JRE_HOME/lib/ext目录下加载jar文件。
	* 可以使用-Djava.ext.dirs命令修改系统属性java.ext.dirs来修改扩展目录。
	* 在Sun的实现中，它是sun.misc.Launcher$ExtClassLoader的实例(事实上它是sun.misc.Launcher类的一个内部类)。
	* 在编写代码中。你可能读取(只能够读取!)系统通属性java.ext.dirs来寻找哪个目录是扩展目录。你不能在在运行期间修改这个属性-即使你修改了修改也不会生效。


3. 应用类加载器
	* 从应用的classpath中加载类。
	* 使用环境变量CLASSPATH(者-cp或者-classpath选项设置应用的classpath，如果CLASSPATH和-cp都找不到,则使用"."(当前目录)。
	* 只读系统属性java.class.path是应用类路径。你不能在运行期间修改这个属性-即使你修改了修改也不会生效。
	* java.lang.ClassLoader.getSystemClassLoader()方法的返回值是这个加载器
	* 这个加载器也叫做"系统加载器"-不过不要将加载java"系统"类的启动加载器混淆。
	* 这个加载器加载你应用的"main"(由main方法的类)。在Sun的实现中,它是sun.misc.Launcher$AppClassLoader的一个实例(事实上它是sun.misc.Launcher类的一个内部类)。
	* 默认的应用加载器用扩展加载器做为它的父加载器。
	* 你可以使用-Djava.system.class.loader命令更改应用的类加载器。这个值指定java.lang.ClassLoader的子类的名字.首先默认应用加载器加载已命名的类(这个类在CLASSPATH或者-cp)和创建一个它的实例.新创建的这个类的实例用于加载应用的main类。


## 一个类典型的类记载流程

让我们假设你正在运行一个"hello world" java程序。我们来看一下类的加载流程。JVM用应用类加载器加载主方法(main)所在的类。如果你运行下面的程序


	class Main {
		public static void main(String[] args) {
            System.out.println(Main.class.getClassLoader());
            javax.swing.JFrame f = new javax.swing.JFrame();
            f.setVisible(true);
            SomeAppClass s = new SomeAppClass();
	}


它会打印如下内容
sun.misc.Launcher$AppClassLoader@17943a4

每当一些其它的类引用在Main类中被解析时，JVM用Main所在类的明确的加载器-应用类加载器-做为初始化加载器。在上面的列子中,为了加载javax.swing.JFrame类JVM将使用应用类加载器做为一个初始化加载器。即，JVM将用应用类应用做为初始化加载器。即。JVM将调用loadClass()方法(loadClassInternal方法)在应用类加载器中。应用类加载器委托给扩展类加载器。
扩展加载器检查这是否是一个启动类(用私有方法 - ClassLoader.findBootstrapClass)，启动类加载器是否从rt.jar加载过它。
当SomeAppClass的引用类被解析时，JVM有着相同的过程-用应用类加载器做为初始化加载器。
应用加载器委托给扩展加载器，扩展加载器检查启动加载器，启动加载器找不到"SomeAppClass"类，
于是扩展加载器检查"SomeAppClass"类是否在扩展jars里，结果发现不在。
于是应用类加载器检查在应用的CLASSPATH下的.class字节，如果找到了则进行加载，如果没有找到，将会抛出NoClassDefFoundError异常。

## 总结:

* Class是由具体的类加载器与类的完全限定类名唯一定义的。

* 如果具体的类加载器不同，即使.class字符是从文件系统中的相同位置进行加载的Classes也是不同的。

* 类加载器委托给父加载器进行加载。

* 加载Bar类中引用的Foo类，JVM使用Bar类的确切的类加载器做为初始化加载器。JVM会在Bar类的确切加载器上会调用loadClass()方法加载Foo类。

* JVM缓存->运行时的类每次初始化加载都将被记录。JVM将会缓存用于以后的解析。即,loadClass()方法不会对于每一次引用都调用。这能确保时间的不变性-即，一个类加载器不允许加载相同类名但字节码不同的类。
他是由缓存来实现的。好的类加载器应该通过调用ClassLoader得call()方法来检查缓存。

## 原文链接
Understanding Java class loading <https://blogs.oracle.com/sundararajan/entry/understanding_java_class_loading>

