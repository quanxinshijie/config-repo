# 1. 安装Java
```
[root@bossvm50 ~] yum install -y java-1.8.0-openjdk.x86_64 java-1.8.0-openjdk-devel.x86_64
[root@bossvm50 ~] java -version
openjdk version "1.8.0_191"
OpenJDK Runtime Environment (build 1.8.0_191-b12)
OpenJDK 64-Bit Server VM (build 25.191-b12, mixed mode)

```

# 2. install cronolog
```
yum -y install gcc gcc-c++ autoconf pcre pcre-devel make automake
```
从 https://fossies.org/linux/www/old/cronolog-1.6.2.tar.gz 下载cronolog，或者将owncloud“移动版\运维方案\tools“下cronolog-1.6.2.tar.gz上传至服务器。

```
[root@bossvm50 ~] tar zxvf cronolog-1.6.2.tar.gz
[root@bossvm50 ~] cd cronolog-1.6.2
[root@bossvm50 cronolog-1.6.2] ./configure
[root@bossvm50 cronolog-1.6.2] make
[root@bossvm50 cronolog-1.6.2] make install
```

# 3. 创建账户
```
[root@bossvm45 ~]# useradd java
[root@bossvm45 ~]# passwd java

everobo2018j
```

# 4. 安装tomcat
```
[root@bossvm45 ~]# su - java
```
上传owncloud“移动版\运维方案\tools”下apache-tomcat-8.0.36.zip至服务器，然后解压。
```
    [root@bossvm50 ~]# yum install -y unzip
    [root@bossvm50 ~]# unzip apache-tomcat-8.0.36.zip -d apache-tomcat-8.0.36
    
```

如果已有tomcat环境，到已有环境的服务器直接通过scp到目标地址。
```
scp -r apache-tomcat-8.0.36 java@192.168.16.40:/home/java
```

设置CATALINA_BASE
```
[java@localhost ~]$ vi ~/.bash_profile

CATALINA_BASE=/home/java/apache-tomcat-8.0.36
PATH=$PATH:$HOME/bin

export PATH CATALINA_BASE


[java@localhost ~]$ source ~/.bash_profile
```

# 5. tomcat调优
1. /home/java/apache-tomcat-8.0.36/bin/setenv.sh
```
JAVA_OPTS="$JAVA_OPTS -server -Xms4g -Xmx4g -verbose:gc -XX:+PrintGC -XX:+PrintGCDetails -XX:+PrintGCDateStamps -XX:+PrintHeapAtGC -XX:+HeapDumpOnOutOfMemoryError -XX:+DisableExplicitGC -Xloggc:$CATALINA_BASE/logs/tomcat_gc.log"
JAVA_OPTS="$JAVA_OPTS -Dprofiles_dir=$CATALINA_BASE/appconf"
JAVA_OPTS="$JAVA_OPTS -Dlog4j.configurationFile=$CATALINA_BASE/appconf/log4j2.xml"
JAVA_OPTS="$JAVA_OPTS -DLog4jContextSelector=org.apache.logging.log4j.core.async.AsyncLoggerContextSelector"
JAVA_OPTS="$JAVA_OPTS -Djava.security.egd=file:/dev/urandom"
JAVA_OPTS="$JAVA_OPTS -Dcom.sun.management.jmxremote"
JAVA_OPTS="$JAVA_OPTS -Dcom.sun.management.jmxremote.port=8999"
JAVA_OPTS="$JAVA_OPTS -Dcom.sun.management.jmxremote.authenticate=false"
JAVA_OPTS="$JAVA_OPTS -Dcom.sun.management.jmxremote.ssl=false"
JAVA_OPTS="$JAVA_OPTS -Djava.rmi.server.hostname=192.168.16.39"
```
通常将-Xms和-Xmx设置成一样，堆的最大值设置为物理可用内存的最大值的80%。

2. /home/java/apache-tomcat-8.0.36/conf/server.xml

```
<Executor name="tomcatThreadPool" namePrefix="catalina-exec-" maxThreads="200" minSpareThreads="50" maxIdleTime="60000" />

<Connector executor="tomcatThreadPool" port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />
```


# 6. 安装nginx

查看CentOS版本信息：
```
[root@bossvm ~]# cat /etc/issue
CentOS release 6.10 (Final)
Kernel \r on an \m
```

打开http://nginx.org/en/linux_packages.html，找到“
Pre-Built Packages for Stable version”，创建nginx的repo
```
[root@bossvm ~]# touch /etc/yum.repos.d/nginx.repo
[root@bossvm ~]# vi /etc/yum.repos.d/nginx.repo


[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/6/$basearch/
gpgcheck=0
enabled=1

[root@bossvm ~]# yum -y install nginx 

```
