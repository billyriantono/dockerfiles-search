FROM tomcat:9-jdk8-openjdk-slim

RUN set -eu ; \
    rm -rf $CATALINA_HOME/bin/*.bat ; \
    rm -Rf $CATALINA_HOME/webapps/*

COPY showcase-6.2.war $CATALINA_HOME/webapps/