FROM centos:latest
RUN yum install -y wget &&\
    wget https://mirrors.cnnic.cn/apache/tomcat/tomcat-8/v8.5.49/bin/apache-tomcat-8.5.49.tar.gz &&\
    tar -zxvf apache-tomcat-8.5.49.tar.gz &&\
    yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel
ADD catalina.sh /apache-tomcat-8.5.49/bin
ADD AnyChat.war /apache-tomcat-8.5.49/webapps
WORKDIR /apache-tomcat-8.5.49/bin
RUN chmod 777 *.sh
ENTRYPOINT [ "./catalina.sh","run" ]
