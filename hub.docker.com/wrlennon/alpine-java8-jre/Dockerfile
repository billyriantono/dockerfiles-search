FROM alpine:3.5

LABEL maintainer "wrlennon"

# Java Version
ENV JAVA_VERSION_MAJOR 8
ENV JAVA_VERSION_MINOR 121
ENV JAVA_VERSION_BUILD 13
ENV JAVA_PACKAGE       jre
ENV JAVA_SHA256_SUM 30bf5fbac0cfbc9201cac1d6973dbc96e5f55043ab315eda8c7aeb23df4f2644
ENV JAVA_URL_ELEMENT   e9e7ea248e2c4826b92b3f075a80e441

# Update curl
# Install glibc-2.21 which is a hard dependency of Java 8. and see https://github.com/mesosphere/kubernetes-mesos/issues/801
# Download the Oracle JRE using tricks in this SO article.
# Remove spurious folders not needed (like jre/lib).
# Set the proper environment variables.

RUN apk add --update curl &&\
    curl -Ls https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.21-r2/glibc-2.21-r2.apk > /tmp/glibc-2.21-r2.apk &&\
    apk add --allow-untrusted /tmp/glibc-2.21-r2.apk &&\
    mkdir -p /opt &&\
    curl -jkLH "Cookie: oraclelicense=accept-securebackup-cookie" -o java.tar.gz\
    http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${JAVA_URL_ELEMENT}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz &&\
    echo "$JAVA_SHA256_SUM  java.tar.gz" | sha256sum -c - &&\
    gunzip -c java.tar.gz | tar -xf - -C /opt && rm -f java.tar.gz &&\
    ln -s /opt/jre1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/jre &&\
    rm -rf /opt/jre/lib/plugin.jar \
         /opt/jre/lib/ext/jfxrt.jar \
         /opt/jre/bin/javaws \
         /opt/jre/lib/javaws.jar \
         /opt/jre/lib/desktop \
         /opt/jre/plugin \
         /opt/jre/lib/deploy* \
         /opt/jre/lib/*javafx* \
         /opt/jre/lib/*jfx* \
         /opt/jre/lib/amd64/libdecora_sse.so \
         /opt/jre/lib/amd64/libprism_*.so \
         /opt/jre/lib/amd64/libfxplugins.so \
         /opt/jre/lib/amd64/libglass.so \
         /opt/jre/lib/amd64/libgstreamer-lite.so \
         /opt/jre/lib/amd64/libjavafx*.so \
         /opt/jre/lib/amd64/libjfx*.so &&\
      apk del curl &&\
      rm -rf /var/cache/apk/*

# Set environment
ENV JAVA_HOME /opt/jre
ENV PATH ${PATH}:${JAVA_HOME}/bin