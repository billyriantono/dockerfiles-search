FROM asuuto/ci-build:latest
LABEL maintainer="Nate Wilken <wilken@asu.edu>"

ENV TOMCAT_MAJOR 7
ENV TOMCAT_VERSION 7.0.94
ENV TOMCAT_TGZ_URL https://www.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz
ENV DBCP_VERSION 7.0.94
ENV DBCP_JAR https://repo1.maven.org/maven2/org/apache/tomcat/tomcat-dbcp/$DBCP_VERSION/tomcat-dbcp-$DBCP_VERSION.jar

WORKDIR /usr/local/tomcat
RUN apk update \
 && apk add --no-cache openjdk8 apache-ant \
 && apk add --no-cache --virtual .build-deps gnupg \
 && curl -sfSL "$TOMCAT_TGZ_URL" -o tomcat.tar.gz \
 && curl -sfSL "$TOMCAT_TGZ_URL.asc" -o tomcat.tar.gz.asc \
 && gpg --keyserver ha.pool.sks-keyservers.net --recv-key A9C5DF4D22E99998D9875A5110C01C5A2F6059E7 \
 && gpg --verify tomcat.tar.gz.asc tomcat.tar.gz \
 && tar xf tomcat.tar.gz --strip-components=1 \
 && rm bin/*.bat \
 && rm tomcat.tar.gz* \
 && curl -sfSL "$DBCP_JAR" -o lib/tomcat-dbcp-$DBCP_VERSION.jar \
 && chown -R 1000:1000 . \
 && rm -rf /root/.gnupg \
 && apk del --purge --no-cache .build-deps

ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

WORKDIR /build
COPY build/build.xml .
COPY build/Dockerfile_7-jre8 Dockerfile
RUN chown -R 1000:1000 .
