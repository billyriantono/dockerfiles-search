FROM alpine:latest

MAINTAINER Madhukar Thota <madhukar.thota@gmail.com>

ENV MAVEN_HOME="/usr/share/maven" \
    JAVA_HOME="/usr/lib/jvm/default-jvm" \
    ZK_VERSION=3.4.10 \
    JAVA_PREFS="/.java/.userPrefs" \
    ZK_HOME="/opt/zookeeper" \
    EXBT_HOME="/opt/exhibitor"

ENV PATH=${JAVA_HOME}/bin:${PATH}

# Update image and install base packages
RUN apk update && \
    apk upgrade && \
    apk add --no-cache bash curl openjdk8 maven && \
    mkdir -p ${EXBT_HOME} && \

    # Default DNS Cache TTL is -1. DNS records, change the default TTL
    grep '^networkaddress.cache.ttl=' ${JAVA_HOME}/jre/lib/security/java.security || echo 'networkaddress.cache.ttl=60' >> ${JAVA_HOME}/jre/lib/security/java.security && \
    
    # Install Zookeeper
    mkdir -p ${ZK_HOME}/transactions ${ZK_HOME}/snapshots && \
    curl -sO http://archive.apache.org/dist/zookeeper/stable/zookeeper-${ZK_VERSION}.tar.gz && \
    tar xzf zookeeper-${ZK_VERSION}.tar.gz  -C ${ZK_HOME} --strip-components=1 && \
    ln -sf /dev/stdout /opt/zookeeper/zookeeper.out && \
    rm -rf zookeeper-*

# Install Exhibitor
ADD pom.xml ${EXBT_HOME}/pom.xml

RUN curl -kL https://raw.github.com/Netflix/exhibitor/master/exhibitor-standalone/src/main/resources/buildscripts/standalone/maven/pom.xml -o ${EXBT_HOME}/pom.xml && \
    mvn -f ${EXBT_HOME}/pom.xml clean package && \
    ln -s ${EXBT_HOME}/target/exhibitor*.jar ${EXBT_HOME}/exhibitor.jar && \
    chown -R nobody:nobody ${ZK_HOME} ${EXBT_HOME}

# To Store Java Preferences
RUN mkdir -p ${JAVA_PREFS} && \
    chown -R nobody:nobody ${JAVA_PREFS}

# Cleanup
RUN apk del curl maven && \
    rm -rf /var/cache/apk/*

# Add the wrapper script to setup configs and exec exhibitor
ADD wrapper.sh ${EXBT_HOME}/wrapper.sh

USER nobody
WORKDIR ${EXBT_HOME}
EXPOSE 2181 2888 3888 8181
ENTRYPOINT ["bash", "-ex", "/opt/exhibitor/wrapper.sh"]
