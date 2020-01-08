FROM centos:7

MAINTAINER lint <lint@heerit.com>


ENV LANG zh_CN.UTF-8 
RUN rm -f /etc/localtime; ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  \
    && yum update -y  \
		&& yum install -y \
    	tar \
   		 wget  \
		&& mkdir /opt/heer  \
		&& cd /opt/heer \
    && wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/6u45-b06/jdk-6u45-linux-x64.bin" \
    && chmod 755 ./*  \
    && ./jdk-6u45-linux-x64.bin  \
    && rm ./jdk-6u45-linux-x64.bin 
ENV JAVA_HOME /opt/heer/jdk1.6.0_45
ENV JAVA_BIN /usr/java/jdk1.6.0_45/bin
ENV JRE_HOME $JAVA_HOME/jre
ENV PATH $PATH:$JAVA_HOME/bin
ENV CLASSPATH .:$JAVA_HOME/lib/dt.jar;$JAVA_HOME/lib/tools.jar