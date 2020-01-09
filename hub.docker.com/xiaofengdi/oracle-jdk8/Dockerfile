FROM xiaofengdi/alpine-glibc:latest
MAINTAINER xiaofeng.di <w5750584@gmail.com>
RUN apk add --no-cache curl tar  && \
    curl -jksSLH "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u144-b01/090f390dda5b47b9b721c7dfaa008135/jdk-8u144-linux-x64.tar.gz -o /tmp/jdk-8u144-linux-x64.tar.gz  && \
    tar zxvf  /tmp/jdk-8u144-linux-x64.tar.gz && \
    mv jdk1.8.0_144 /usr/java && \
    rm -rf /tmp/* && \
    rm -rf /var/cache/apk/* && \
    apk del curl tar
ENV JAVA_HOME=/usr/java/ \
    CLASSPATH=$JAVA_HOME/lib \
    LANG=en_US.UTF8 
ENV PATH=${JAVA_HOME}/bin:${PATH}
