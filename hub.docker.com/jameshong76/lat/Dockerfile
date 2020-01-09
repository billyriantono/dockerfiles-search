FROM httpd:2.4-alpine

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH

RUN apk add openjdk8 \
    && cd /usr/local \
    && wget http://apache.mirror.cdnetworks.com/tomcat/tomcat-7/v7.0.96/bin/apache-tomcat-7.0.96.tar.gz \
    && tar xvfz apache-tomcat-7.0.96.tar.gz \ 
    && mv apache-tomcat-7.0.96 tomcat \
    && apk add curl

EXPOSE 8080

COPY httpd-foreground /usr/local/bin/
COPY cmd.sh /usr/local/bin/

CMD ["cmd.sh"]
