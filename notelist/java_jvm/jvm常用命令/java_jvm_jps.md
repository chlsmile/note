## jvm常用命令jps

NAME
       jps - Lists the instrumented Java Virtual Machines (JVMs) on the target system. This command is experimental and unsupported.

SYNOPSIS
       jps [ options ] [ hostid ]

       options
              Command-line options. See Options.

       hostid The identifier of the host for which the process report should be generated. The hostid can include optional components that indicate the communications protocol, port number, and other
              implementation specific data. See Host Identifier.

DESCRIPTION
       The jps command lists the instrumented Java HotSpot VMs on the target system. The command is limited to reporting information on JVMs for which it has the access permissions.

       If the jps command is run without specifying a hostid, then it searches for instrumented JVMs on the local host. If started with a hostid, then it searches for JVMs on the indicated host, using the
       specified protocol and port. A jstatd process is assumed to be running on the target host.

       The jps command reports the local JVM identifier, or lvmid, for each instrumented JVM found on the target system. The lvmid is typically, but not necessarily, the operating system's process
       identifier for the JVM process. With no options, jps lists each Java application's lvmid followed by the short form of the application's class name or jar file name. The short form of the class
       name or JAR file name omits the class's package information or the JAR files path information.

       The jps command uses the Java launcher to find the class name and arguments passed to the main method. If the target JVM is started with a custom launcher, then the class or JAR file name and the
       arguments to the main method are not available. In this case, the jps command outputs the string Unknown for the class name or JAR file name and for the arguments to the main method.

       The list of JVMs produced by the jps command can be limited by the permissions granted to the principal running the command. The command only lists the JVMs for which the principle has access
       rights as determined by operating system-specific access control mechanisms.

OPTIONS
       The jps command supports a number of options that modify the output of the command. These options are subject to change or removal in the future.

       -q
              Suppresses the output of the class name, JAR file name, and arguments passed to the main method, producing only a list of local JVM identifiers.

       -m
              Displays the arguments passed to the main method. The output may be null for embedded JVMs.

       -l
              Displays the full package name for the application's main class or the full path name to the application's JAR file.

       -v
              Displays the arguments passed to the JVM.

       -V
              Suppresses the output of the class name, JAR file name, and arguments passed to the main method, producing only a list of local JVM identifiers.

       -Joption
              Passes option to the JVM, where option is one of the options described on the reference page for the Java application launcher. For example, -J-Xms48m sets the startup memory to 48 MB. See
              java(1).

HOST IDENTIFIER
       The host identifier, or hostid is a string that indicates the target system. The syntax of the hostid string corresponds to the syntax of a URI:

       [protocol:][[//]hostname][:port][/servername]