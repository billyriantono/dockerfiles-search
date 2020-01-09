FROM ubuntu:16.04
MAINTAINER Cornel

ENV DEBIAN_FRONTEND noninteractive
ENV TOMCAT tomcat7

# install Java 8, Tomcat 8, supervisor
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" > /etc/apt/sources.list.d/webupd8team-java.list \
    && echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" >> /etc/apt/sources.list.d/webupd8team-java.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 \
    && apt-get -y update \
    && echo debconf shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections \
    && apt-get -y install oracle-java8-installer oracle-java8-set-default \
    && apt-get -y install ${TOMCAT} \
    && apt-get -y install supervisor \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean \
    && mkdir /tmp/spark-events

# Tomcat7 startup script looks for Java in the folders:
#   • /usr/lib/jvm/java-${java_version}-openjdk-*
#   • /usr/lib/jvm/jdk-${java_version}-oracle-*
#   • /usr/lib/jvm/jre-${java_version}-oracle-*
#   • /usr/lib/jvm/java-6-openjdk
#   • /usr/lib/jvm/java-6-sun
#   • /usr/lib/jvm/java-7-oracle
#   • /usr/lib/jvm/default-java
# However, Java 8 is installed in /usr/lib/jvm/java-8-oracle,
#   which is not in the list. This is why we need to make a
#   symbolic link from "default-java" to "java-8-oracle".
#RUN ln -s /usr/lib/jvm/java-8-oracle /usr/lib/jvm/default-java

# copy tomcat configuration file
#COPY tomcat8/context.xml /var/lib/tomcat8/conf/context.xml
#COPY tomcat8/setenv.sh /usr/share/${TOMCAT}/bin/setenv.sh

# copy some scripts to run Tomcat
COPY scripts/start-tomcat.sh /usr/bin/start-tomcat.sh

# Supervisor config
COPY supervisor/tomcat.conf /etc/supervisor/conf.d/

# copy the Legis webapp
# - legis.webapp.war: the new version of Legis, where the SparkDriver runs inside Tomcat8.
#   The available URLs are:
#   • /legis.webapp/pi
#   • /legis.webapp/directions
# - webapp-legis.war: the old verion of Legus, where Spark is called using a hidden
#   REST API. The driver starts on Spark, and making a lot of requests can lead to
#   a deadlock between the Driver and Executors. The available URLs are:
#   • /webapp-legis/rest/directions/pi
#   • /webapp-legis/rest/directions
#COPY webapp/webapp-legis.war /var/lib/tomcat8/webapps/webapp-legis.war
COPY webapp/legis.webapp.war /var/lib/${TOMCAT}/webapps/legis.webapp.war

# configure tomcat connections to Spark and Cassandra
ENV SPARK_MASTER="spark-master"
ENV CASSANDRA="cassandra-01"
ENV LOAD_BALANCER="load-balancer"

### Tomcat ports
# 8080: default website
# 4040: port open by the SparkDriver
EXPOSE 8080 4040

# by default, this container is a Spark Worker
CMD ["supervisord", "-n"]
