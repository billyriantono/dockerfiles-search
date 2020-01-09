FROM tomcat

ENV CATALINA_BASE /usr/local/tomcat/
ENV CATALINA_HOME /usr/local/tomcat
ENV CATALINA_TMPDIR /usr/local/tomcat/temp
 
LABEL maintainer="Subin Mathew https://github.com/subinamathew/magnolia-docker"

RUN apt-get update && apt-get -y dist-upgrade

RUN apt-get install -qq -y mysql-client

RUN rm -rf $CATALINA_BASE/webapps/*

COPY tomcat/setenv.sh $CATALINA_BASE/bin/setenv.sh
COPY tomcat/catalina.properties  $CATALINA_BASE/conf/catalina.properties
COPY tomcat/context.xml $CATALINA_BASE/conf/context.xml