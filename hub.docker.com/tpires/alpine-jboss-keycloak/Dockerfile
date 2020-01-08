# Use latest tpires/alpine-openjdk:8 image as the base
FROM tpires/alpine-openjdk:8
MAINTAINER Tiago Pires <tandrepires@gmail.com>

ENV JBOSS_HOME /opt/jboss/keycloak
# Set KEYCLOAK_VERSION
ENV KEYCLOAK_VERSION 1.5.0.Final
# Gracefully shutdown Keycloak
ENV LAUNCH_JBOSS_IN_BACKGROUND 1

# Set user root to install dependencies
USER root
RUN apk add --update jq && \
    rm /var/cache/apk/*
RUN mkdir -p /usr/share/java/saxon
RUN curl -L -o /usr/share/java/saxon/saxon.zip http://downloads.sourceforge.net/project/saxon/Saxon-HE/9.6/SaxonHE9-6-0-7J.zip && \
    unzip /usr/share/java/saxon/saxon.zip -d /usr/share/java/saxon && \
    rm -rf /usr/share/java/saxon/noticies /usr/share/java/saxon/doc \
      /usr/share/java/saxon/saxon9-test.jar /usr/share/java/saxon/saxon9-unpack.jar /usr/share/java/saxon/saxon.zip
USER jboss

RUN cd /opt/jboss && \
    curl -L https://downloads.jboss.org/keycloak/$KEYCLOAK_VERSION/keycloak-$KEYCLOAK_VERSION.tar.gz | \
    tar zx && mv /opt/jboss/keycloak-$KEYCLOAK_VERSION /opt/jboss/keycloak

ADD setLogLevel.xsl $JBOSS_HOME/
RUN java -jar /usr/share/java/saxon/saxon9he.jar -s:/opt/jboss/keycloak/standalone/configuration/standalone.xml \
      -xsl:/opt/jboss/keycloak/setLogLevel.xsl -o:/opt/jboss/keycloak/standalone/configuration/standalone.xml

EXPOSE 8080

CMD ["/opt/jboss/keycloak/bin/standalone.sh", "-b", "0.0.0.0"]
