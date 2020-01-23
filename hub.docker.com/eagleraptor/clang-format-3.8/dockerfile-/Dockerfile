# e4Cash DOCKERFILES PROJECT
# --------------------------
# This is the Dockerfile for Middleware Wildfly
# 
# HOW TO BUILD THIS IMAGE
# -----------------------
# Put all downloaded files in the same directory as this Dockerfile
# Run: 
#      $ docker build -t e4cash/middleware:12.0.0.Final . 
#
# Pull base image
# ---------------
FROM ubuntu:16.04

# Maintainer
# ----------
LABEL maintainer="jose.schmucke@ab4cus.com"
MAINTAINER Jose A. Schmucke <jose.schmucke@ab4cus.com>

#ADD VERSION .

ENV WILDFLY_VERSION 12.0.0.Final
ENV JBOSS_HOME /opt/jboss/wildfly
ENV JAVA_VERSION_MAJOR 8
ENV JAVA_VERSION_MINOR 131
ENV JAVA_VERSION_BUILD 11
ENV JAVA_HOME /opt/jdk
ENV PATH ${PATH}:${JAVA_HOME}/bin
ENV POSTGRESQL_VERSION 9.4-1201-jdbc41

ARG DB_HOST=postgresql
ARG DB_NAME=e4cash
ARG DB_USER=e4cash
ARG DB_PASS=e41234

#RUN apt-get update
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils iputils-ping
RUN apt-get -qq -y install curl ca-certificates tar wget vim
RUN apt-get -qq -y install software-properties-common 

RUN mkdir -p /opt/jboss/wildfly
RUN groupadd -r wildfly
RUN useradd -r -g wildfly -d /opt/jboss/wildfly -s /sbin/nologin wildfly
RUN chown -R wildfly:wildfly /opt/jboss

# Install Java8 from repository webupd8team/java.
#RUN  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
#  add-apt-repository -y ppa:webupd8team/java && \
#  apt-get update && \
#  apt-get install -y oracle-java8-installer && \
#  rm -rf /var/lib/apt/lists/* && \
#  rm -rf /var/cache/oracle-jdk8-installer

# Install Java8 from oracle (from https://developer.atlassian.com/blog/2015/08/minimal-java-docker-containers/)
RUN  curl -v -j -k -L -H "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/d54c1d3a095b4ff2b6607d096fa80163/jdk-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz | tar -xzf - -C /opt && \
  ln -s /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/jdk && \
  rm -rf /opt/jdk/*src.zip \
       /opt/jdk/lib/missioncontrol \
       /opt/jdk/lib/visualvm \
       /opt/jdk/lib/*javafx* \
       /opt/jdk/jre/lib/plugin.jar \
       /opt/jdk/jre/lib/ext/jfxrt.jar \
       /opt/jdk/jre/bin/javaws \
       /opt/jdk/jre/lib/javaws.jar \
       /opt/jdk/jre/lib/desktop \
       /opt/jdk/jre/plugin \
       /opt/jdk/jre/lib/deploy* \
       /opt/jdk/jre/lib/*javafx* \
       /opt/jdk/jre/lib/*jfx* \
       /opt/jdk/jre/lib/amd64/libdecora_sse.so \
       /opt/jdk/jre/lib/amd64/libprism_*.so \
       /opt/jdk/jre/lib/amd64/libfxplugins.so \
       /opt/jdk/jre/lib/amd64/libglass.so \
       /opt/jdk/jre/lib/amd64/libgstreamer-lite.so \
       /opt/jdk/jre/lib/amd64/libjavafx*.so \
       /opt/jdk/jre/lib/amd64/libjfx*.so && \
 echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf

RUN java -version
RUN which java

USER wildfly

WORKDIR /opt/jboss/wildfly

# Install Wildfly and add an admin user (password admin)
RUN cd /tmp && \
  curl -O https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz && \
  tar xf wildfly-$WILDFLY_VERSION.tar.gz && \
  mkdir -p $JBOSS_HOME && \
  mv /tmp/wildfly-$WILDFLY_VERSION/* $JBOSS_HOME/ && \
  rm -r wildfly-* && \
  $JBOSS_HOME/bin/add-user.sh admin -p admin -s

# Install postgres drivers and datasource
RUN /bin/sh -c '$JBOSS_HOME/bin/standalone.sh &' && \
  sleep 10 && \
  cd /tmp && \
  curl --location --output postgresql-${POSTGRESQL_VERSION}.jar --url http://search.maven.org/remotecontent?filepath=org/postgresql/postgresql/${POSTGRESQL_VERSION}/postgresql-${POSTGRESQL_VERSION}.jar && \
  $JBOSS_HOME/bin/jboss-cli.sh --connect --command="deploy /tmp/postgresql-${POSTGRESQL_VERSION}.jar" && \
  $JBOSS_HOME/bin/jboss-cli.sh --connect --command="xa-data-source add --name=e4cash-postgresql --jndi-name=java:/jdbc/datasources/e4cashDS --user-name=${DB_USER} --password=${DB_PASS} --driver-name=postgresql-9.4-1201-jdbc41.jar --xa-datasource-class=org.postgresql.xa.PGXADataSource --xa-datasource-properties=ServerName=${DB_HOST},PortNumber=5432,DatabaseName=${DB_NAME} --valid-connection-checker-class-name=org.jboss.jca.adapters.jdbc.extensions.postgres.PostgreSQLValidConnectionChecker --exception-sorter-class-name=org.jboss.jca.adapters.jdbc.extensions.postgres.PostgreSQLExceptionSorter" && \
  $JBOSS_HOME/bin/jboss-cli.sh --connect --command=:shutdown && \
  rm -rf $JBOSS_HOME/standalone/configuration/standalone_xml_history/ $JBOSS_HOME/standalone/log/* && \
  rm /tmp/postgresql-9.4*.jar && \
  rm -rf /tmp/postgresql-*.jar


# Expose http and admin ports
EXPOSE 8080 9990

# Set the default command to run on boot
# This will boot WildFly in the standalone mode and bind to all interfaces
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0", "-c", "standalone-full.xml"]

