FROM centos:6

MAINTAINER Jack <17210240149@fudan.edu.cn>

USER root

ENV JAVA_HOME=/usr/lib/jdk8

ENV PATH=$PATH:$JAVA_HOME/bin:.

# 安装 wget,rsync
# 设置系统时区为北京时间（实际为Asia/Shanghai）

RUN yum install -y wget rsync\
    && wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.tar.gz \
    && tar -xzvf jdk-8u181-linux-x64.tar.gz -C /usr/lib/ \
    && mv /usr/lib/jdk1.8.0_181 $JAVA_HOME \
    && rm -rf jdk-8u181-linux-x64.tar.gz $JAVA_HOME/src.zip $JAVA_HOME/javafx-src.zip $JAVA_HOME/man \
    && yum clean all \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN yum install vim -y

CMD ["/bin/bash"]
