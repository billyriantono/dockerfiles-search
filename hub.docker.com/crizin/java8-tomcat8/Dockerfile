FROM frolvlad/alpine-glibc:alpine-3.4

MAINTAINER Crizin <crizin@gmail.com>

ENV JAVA_VERSION=8 \
    JAVA_UPDATE=92 \
    JAVA_BUILD=14 \
    JAVA_HOME="/usr/lib/jvm/default-jvm" \
    CATALINA_HOME="/usr/local/tomcat" \
    TOMCAT_MAJOR=8 \
    TOMCAT_VERSION=8.5.3

RUN apk add --update --no-cache bash && \
    apk add --update --no-cache --virtual=build-dependencies tar wget && \
    cd "/tmp" && \
    wget -q --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
        "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz" && \
    tar -xzf "jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz" && \
    mkdir -p "/usr/lib/jvm" && \
    mv "/tmp/jdk1.${JAVA_VERSION}.0_${JAVA_UPDATE}" "/usr/lib/jvm/java-${JAVA_VERSION}-oracle" && \
    ln -s "java-${JAVA_VERSION}-oracle" "$JAVA_HOME" && \
    ln -s "$JAVA_HOME/bin/"* "/usr/bin/" && \
    rm -rf "$JAVA_HOME/"*src.zip && \
    rm -rf "$JAVA_HOME/lib/missioncontrol" \
           "$JAVA_HOME/lib/visualvm" \
           "$JAVA_HOME/lib/"*javafx* \
           "$JAVA_HOME/jre/lib/plugin.jar" \
           "$JAVA_HOME/jre/lib/ext/jfxrt.jar" \
           "$JAVA_HOME/jre/bin/javaws" \
           "$JAVA_HOME/jre/lib/javaws.jar" \
           "$JAVA_HOME/jre/lib/desktop" \
           "$JAVA_HOME/jre/plugin" \
           "$JAVA_HOME/jre/lib/"deploy* \
           "$JAVA_HOME/jre/lib/"*javafx* \
           "$JAVA_HOME/jre/lib/"*jfx* \
           "$JAVA_HOME/jre/lib/amd64/libdecora_sse.so" \
           "$JAVA_HOME/jre/lib/amd64/"libprism_*.so \
           "$JAVA_HOME/jre/lib/amd64/libfxplugins.so" \
           "$JAVA_HOME/jre/lib/amd64/libglass.so" \
           "$JAVA_HOME/jre/lib/amd64/libgstreamer-lite.so" \
           "$JAVA_HOME/jre/lib/amd64/"libjavafx*.so \
           "$JAVA_HOME/jre/lib/amd64/"libjfx*.so

RUN cd "/tmp" && \
    wget -q "http://apache.mirror.cdnetworks.com/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz" && \
    mkdir -p "$CATALINA_HOME" && \
    cd "$CATALINA_HOME" && \
    tar -xvf "/tmp/apache-tomcat-$TOMCAT_VERSION.tar.gz" --strip-components=1 && \
    rm "bin/"*.bat && \
    sed -i 's/Connector port="8080"/Connector port="8080" URIEncoding="UTF-8"/g' "$CATALINA_HOME/conf/server.xml"

RUN apk del build-dependencies && \
    rm "/tmp/"*

WORKDIR /usr/local/tomcat

EXPOSE 8080

CMD ["bin/catalina.sh", "run"]
