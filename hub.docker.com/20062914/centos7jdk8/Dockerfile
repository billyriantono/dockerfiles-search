FROM centos:7

MAINTAINER lint <lint@heerit.com>


ENV LANG zh_CN.UTF-8 
RUN rm -f /etc/localtime; ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  \
    && yum -y install kde-l10n-Chinese && yum -y reinstall glibc-common \
    && localedef -c -f UTF-8 -i zh_CN zh_CN.utf8 \
    && yum update -y  \
    && yum install -y tar wget  \
    && mkdir /opt/heer  \
    && cd /opt/heer \
    && wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.rpm \
    && chmod 755 ./*  \
    && yum -y install jdk-8u131-linux-x64.rpm  \
    && rm ./jdk-8u131-linux-x64.rpm && yum clean all
ENV JAVA_HOME /usr/java/jdk1.8.0_131
ENV JAVA_BIN /usr/java/jdk1.8.0_131/bin
ENV JRE_HOME $JAVA_HOME/jre
ENV PATH $PATH:$JAVA_HOME/bin
ENV CLASSPATH .:$JAVA_HOME/lib/dt.jar;$JAVA_HOME/lib/tools.jar
