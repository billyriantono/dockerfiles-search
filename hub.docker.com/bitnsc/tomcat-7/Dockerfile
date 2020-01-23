FROM liling/phusion-java:latest

MAINTAINER liling@bit.edu.cn

EXPOSE 8080

ENV TOMCAT_MAJOR_VERSION 7
ENV TOMCAT_MINOR_VERSION 7.0.68
ENV CATALINA_HOME /opt/tomcat
ENV LC_ALL zh_CN.UTF-8

# INSTALL TOMCAT
RUN cd /opt && \
    wget -q http://www.eu.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz -O - | tar zxf - --exclude=webapps --exclude=logs && \
    mv apache-tomcat* tomcat && \
    chown -R www-data tomcat/temp tomcat/work && \
    chmod +r tomcat/conf/*

EXPOSE 8009 8080

ADD unwar.sh /unwar.sh
ADD run.sh /run.sh
RUN chmod +x /*.sh

ENV CATALINA_OPTS "-Xmx2048m -server -XX:MaxPermSize=512m"
WORKDIR '/opt/tomcat'
CMD ["/run.sh"]
