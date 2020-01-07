FROM anapsix/alpine-java:8_jdk_unlimited

MAINTAINER gg  <guogang1984@gmail.com>

ENV TOMCAT_MAJOR=8 \
    TOMCAT_VERSION=8.5.41 \
    TOMCAT_HOME=/opt/tomcat \
    CATALINA_HOME=/opt/tomcat \
    CATALINA_TMPDIR=/tmp/java/tmp \
    CATALINA_OUT=/dev/null \
    MAVEN_VERSION=3.6.1 \
    MAVEN_HOME=/opt/maven \
    JVM_ARGS_OPTS="-Djava.io.tmpdir=/tmp/java/tmp -Djava.security.egd=file:/dev/./urandom -Duser.timezone=GMT+08" \
    JVM_PERFORMANCE_OPTS="-server -Xms512m -Xmx2048m -XX:PermSize=256m -XX:MaxPermSize=512m" \
    PATH=${PATH}:/opt/tomcat/bin:/opt/maven/bin

ENV JAVA_OPTS="${JVM_PERFORMANCE_OPTS} ${JVM_ARGS_OPTS}" 


RUN apk upgrade --update && \
    apk add --update curl unzip && \ 
    curl -jksSL -o /tmp/apache-tomcat.tar.gz http://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
    gunzip /tmp/apache-tomcat.tar.gz && \
    tar -C /opt -xf /tmp/apache-tomcat.tar && \
    ln -s /opt/apache-tomcat-${TOMCAT_VERSION} ${TOMCAT_HOME} && \
    rm -rf ${TOMCAT_HOME}/webapps/* && \
    curl -fsSL -o /tmp/apache-maven.tar.gz https://www-us.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    gunzip /tmp/apache-maven.tar.gz && \
    tar -C /opt -xf /tmp/apache-maven.tar && \
    ln -s /opt/apache-maven-${MAVEN_VERSION} ${MAVEN_HOME} && \
    apk del curl unzip && \
    rm -rf /tmp/* /var/cache/apk/*

COPY alpine/etc/localtime  /etc/localtime

COPY redis-session-lib/* ${TOMCAT_HOME}/lib/

COPY tomcat8/conf/* ${TOMCAT_HOME}/conf/

COPY entrypoint-app.sh /

VOLUME ["/tmp/logs"]

EXPOSE 8080


