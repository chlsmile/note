## jdk install

```bash
#! /bin/bash

# 安装目录/usr/local
# jdk安装包jdk-8u181-linux-x64.tar.gz
# jdk安装包需要提前准备好放置到/usr/local下


echo "cd /usr/local"
cd /usr/local

echo "tar -xzvf jdk-8u181-linux-x64.tar.gz"
tar -xzvf jdk-8u181-linux-x64.tar.gz

echo "mv jdk1.8.0_181 jdk"
mv jdk1.8.0_181 jdk

echo "update /etc/profile"

cat >> /etc/profile  << EOF

#jdk
JAVA_HOME=/usr/local/jdk
PATH=$JAVA_HOME/bin:$PATH
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export JAVA_HOME PATH CLASSPATH

EOF

echo "source /etc/profile"
source /etc/profile

echo "jdk is installed"

echo "java -version"

java -version

```