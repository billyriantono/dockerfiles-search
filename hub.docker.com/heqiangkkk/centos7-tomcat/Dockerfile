FROM centos:7
MAINTAINER Heqiang "heqiangkkk@qq.com"
RUN yum -y install wget ;\
    yum clean all ;\
    wget -P / http://archive.apache.org/dist/tomcat/tomcat-7/v7.0.75/bin/apache-tomcat-7.0.75.tar.gz;\
    wget -P / http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.tar.gz?AuthParam=1496990727_42766fff541576c7eb3c4433553c2916;\
    tar -zxvf apache-tomcat-7.0.75.tar.gz -C /usr/local/;\
    rm -f /apache-tomcat-7.0.75.tar.gz ;\
    tar -zxvf jdk-8u131-linux-x64.tar.gz -C /usr/local/;\
    rm -f /jdk-8u131-linux-x64.tar.gz
    
RUN export JAVA_HOME=/usr/local/jdk1.8.0_131 ;\
    export PATH=$JAVA_HOME/bin:$PATH ;\
    export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar;\
    source /etc/profile

#COPY ./start.sh /
#COPY ./sample1.war /tomcat/webapps/
#RUN chmod +x /start.sh
#EXPOSE 8080
#ENTRYPOINT ["/start.sh"]
