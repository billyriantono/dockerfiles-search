FROM openjdk:12-alpine
ARG WILDFLY_VERSION=18.0.0.Final
ARG WILDFLY_DOWNLOAD_URL=https://download.jboss.org/wildfly/${WILDFLY_VERSION}/servlet/wildfly-servlet-${WILDFLY_VERSION}.tar.gz

RUN wget ${WILDFLY_DOWNLOAD_URL} \
 && tar -zxvf wildfly-servlet-${WILDFLY_VERSION}.tar.gz \
 && rm wildfly-servlet-${WILDFLY_VERSION}.tar.gz \
 && mv wildfly-servlet-${WILDFLY_VERSION} wildfly

WORKDIR /wildfly

EXPOSE 8080