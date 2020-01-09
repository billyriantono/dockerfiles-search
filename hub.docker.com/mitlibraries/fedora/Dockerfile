FROM tomcat:8.5
MAINTAINER Mike Graves <mgraves@mit.edu>

ENV FCREPO_VERSION 4.7.0

ADD setenv.sh $CATALINA_HOME/bin/
RUN mkdir -p /etc/fcrepo/
COPY activemq.xml /etc/fcrepo/
ADD https://github.com/fcrepo4/fcrepo4/releases/download/fcrepo-${FCREPO_VERSION}/fcrepo-webapp-${FCREPO_VERSION}.war \
    $CATALINA_HOME/webapps/fcrepo.war

EXPOSE 61613
