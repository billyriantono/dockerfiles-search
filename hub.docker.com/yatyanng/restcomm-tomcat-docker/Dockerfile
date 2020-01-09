FROM cemmersb/centos-jdk8:1.0.1

MAINTAINER Yan Ng

RUN yum -y install unzip
RUN adduser -m tomcat
USER tomcat

WORKDIR /home/tomcat

RUN wget -q https://github.com/yatyanng/restcomm-sip-servlets-4.0.128-apache-tomcat-8.0.26/archive/master.zip 
RUN unzip -q master.zip 
RUN mv restcomm-sip-servlets-4.0.128-apache-tomcat-8.0.26-master restcomm-tomcat 
RUN rm master.zip

ENV DEBUG_PORT=8091
ENV ADMIN_USERNAME=admin
ENV ADMIN_PASSWORD=admin
ENV SIP_PORT=5060
ENV HTTP_PORT=8090
ENV CATALINA_HOME=/home/tomcat/restcomm-tomcat

EXPOSE 5060/udp
EXPOSE 5060/tcp
EXPOSE 8090/tcp
EXPOSE 8091/tcp
 
WORKDIR $CATALINA_HOME

RUN mkdir -p $CATALINA_HOME/logs
RUN cat bin/setenv.sh | sed s/\$SIP_ADDRESS/$(ip address show eth0 | grep -oP 'inet [0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' | sed 's/inet //g')/g >> bin/setenv2.sh ; mv bin/setenv2.sh bin/setenv.sh
RUN echo "DEBUG_PORT: $DEBUG_PORT" >> $CATALINA_HOME/logs/environment.log
RUN echo "ADMIN_USERNAME: $ADMIN_USERNAME" >> $CATALINA_HOME/logs/environment.log
RUN echo "SIP_PORT: $SIP_PORT" >> $CATALINA_HOME/logs/environment.log
RUN echo "HTTP_PORT: $HTTP_PORT" >> $CATALINA_HOME/logs/environment.log
RUN echo "CATALINA_HOME: $CATALINA_HOME" >> $CATALINA_HOME/logs/environment.log
CMD ["/home/tomcat/restcomm-tomcat/bin/catalina.sh", "run"]

