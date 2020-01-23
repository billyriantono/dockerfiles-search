FROM debian:latest

ENV JAVA_VERSION=8 \
    JAVA_UPDATE=66 \
    JAVA_BUILD=17 \
    JAVA_MODE=jdk \
    JAVA_HOME=/opt/java

RUN apt-get update && \
    apt-get install -y wget

RUN cd /tmp && \
    wget --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
        "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/${JAVA_MODE}-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz" && \
    tar xzvf "${JAVA_MODE}-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz" -C /opt && \
    ln -s "/opt/${JAVA_MODE}1.${JAVA_VERSION}.0_${JAVA_UPDATE}" $JAVA_HOME && \
    ln -s $JAVA_HOME/bin/java /usr/bin/java && \
    chown -R root:root "/opt/${JAVA_MODE}1.${JAVA_VERSION}.0_${JAVA_UPDATE}"
