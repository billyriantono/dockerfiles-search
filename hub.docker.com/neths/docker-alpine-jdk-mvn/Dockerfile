FROM anapsix/alpine-java:8_jdk

MAINTAINER Neths <vacher.michel@gmail.com>

ENV MAVEN_VERSION="3.3.9"
ENV M2_HOME=/usr/lib/mvn

RUN apk --no-cache add wget openssl ca-certificates && \

    ## Get security
    mkdir -p "$JAVA_HOME/lib/ext/" && \
    cd "$JAVA_HOME/lib/ext/" && \
    wget http://downloads.bouncycastle.org/java/bcprov-ext-jdk15on-152.jar && \
    mkdir -p "$JAVA_HOME/lib/security" && \
    cd "$JAVA_HOME/lib/security" && \
    echo 'security.provider.10=org.bouncycastle.jce.provider.BouncyCastleProvider' >> "$JAVA_HOME/lib/security/java.security" && \

    ## Get maven
    wget "https://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz" && \
    tar -zxvf "apache-maven-$MAVEN_VERSION-bin.tar.gz" && \
    mv "apache-maven-$MAVEN_VERSION" "$M2_HOME" && \
    ln -s "$M2_HOME/bin/mvn" /usr/bin/mvn


ENV BUILD_DIR /build

RUN mkdir -p ${BUILD_DIR}

WORKDIR /

VOLUME ["/build_out", "/build_in"]

ADD build.sh /build.sh

RUN chmod u+x /build.sh

ENV BUILD_TARGET "clean install"
ENV BUILD_OPTIONS "-Dmaven.javadoc.skip=true -DskipTests -T 2C"

ENTRYPOINT ["/build.sh"]