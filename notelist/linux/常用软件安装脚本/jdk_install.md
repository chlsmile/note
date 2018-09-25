## jdk install

```
#! /bin/bash

# 安装目录/usr/local
# jdk安装包jdk-8u181-linux-x64.tar.gz
# jdk安装包需要提前准备好放置到/usr/local下


echo "cd /usr/local"
cd /usr/local


echo "tar -xzf jdk-8u181-linux-x64.tar.gz"
tar -xzf jdk-8u181-linux-x64.tar.gz


echo "mv jdk1.8.0_181 jdk8"
mv jdk1.8.0_181 jdk8

echo "update /etc/profile"

cat >> /etc/profile  << EOF

# JAVA
JAVA_HOME=/usr/local/jdk8
JRE_HOME=\$JAVA_HOME/jre
PATH=\$PATH:\$JAVA_HOME/bin:\$JRE_HOME/bin
CLASSPATH=.:\$JAVA_HOME/lib/dt.jar:\$JAVA_HOME/lib/tools.jar:\$JRE_HOME/lib

EOF

echo "source /etc/profile"
source /etc/profile

echo "jdk is installed"

echo "java -version"

java -version

```