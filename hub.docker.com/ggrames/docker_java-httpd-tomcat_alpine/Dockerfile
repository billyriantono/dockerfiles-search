# java httpd and tomcat 
FROM alpine
MAINTAINER Gernot Grames <gernot.grames@gmx.at>
ENV container docker
ENV UPDATED_ON "10 December 2016"
ENV TOMCAT_VERSION 8.0.39

RUN apk add --update apache2 apache2-proxy bash wget tar supervisor

# apache
RUN mkdir -p /run/apache2/
RUN chown -R apache:apache /run/apache2/

# install java
RUN apk --update add openjdk8

# install tomcat
RUN wget -q https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_VERSION%%.*}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz
RUN wget -qO- https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_VERSION%%.*}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz.md5 | md5sum -c -
RUN mkdir -p /opt
RUN tar xzf apache-tomcat-${TOMCAT_VERSION}.tar.gz -C /opt
RUN ln -s /opt/apache-tomcat-${TOMCAT_VERSION} /opt/tomcat

# cleanup
RUN rm apache-tomcat-${TOMCAT_VERSION}.tar.gz
RUN apk del wget
RUN apk del tar

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY httpd.conf /etc/apache2/httpd.conf

EXPOSE 80
EXPOSE 443

CMD /usr/bin/supervisord -c /etc/supervisor/conf.d/supervisord.conf
