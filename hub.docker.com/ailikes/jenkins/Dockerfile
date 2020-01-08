#Tomcat docker file from ailikes
#VERSION 0.0.1
#Author: ailikes

FROM registry.cn-beijing.aliyuncs.com/ailikes_tools/alpine-openjdk8:latest
#作者
MAINTAINER ailikes <15600499930@163.com>
ENV CATALINA_HOME /tomcat
ADD jenkins_tomcat /tomcat
ADD run.sh /run.sh
RUN chmod +x /*.sh
RUN chmod +x /tomcat/bin/*.sh
EXPOSE 18080
CMD ["/run.sh"]
