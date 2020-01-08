#Tomcat docker file from ailikes
#VERSION 0.0.1
#Author: ailikes

FROM daocloud.io/library/centos:latest
#作者
MAINTAINER ailikes <15600499930@163.com>
COPY jdk1.8  /usr/local/jdk1.8/
ADD tomcat /tomcat
ADD run.sh /run.sh

ENV JAVA_HOME /usr/local/jdk1.8
ENV CATALINA_HOME /tomcat
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin

RUN chmod +x /*.sh
RUN chmod +x /tomcat/bin/*.sh
EXPOSE 18080
CMD ["/run.sh"]
