FROM  idasound/centos7-jdk8

MAINTAINER Brand Idasound "haowang@idasound.com"

RUN mkdir -p  /home/tomcat/

WORKDIR /home/tomcat/
RUN wget http://qx24.cn/apache-tomcat-7.0.82.tar.gz
RUN  tar zxvf apache-tomcat-7.0.82.tar.gz
RUN  rm -rf  apache-tomcat-7.0.82.tar.gz

RUN rm -rf\
  /home/tomcat/apache-tomcat-7.0.82/webapps/docs \
  /home/tomcat/apache-tomcat-7.0.82/webapps/examples \
  /home/tomcat/apache-tomcat-7.0.82/webapps/ROOT \
  /home/tomcat/apache-tomcat-7.0.82/webapps/host-manager \
  /home/tomcat/apache-tomcat-7.0.82/webapps/manager

ENV TIME_ZONE              Asia/Shanghai


CMD ["apache-tomcat-7.0.82/bin/catalina.sh","run"]
