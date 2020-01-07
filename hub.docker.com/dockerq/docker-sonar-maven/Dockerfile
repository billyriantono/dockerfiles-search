FROM sonarqube:6.7
MAINTAINER adolphlwq

# ref https://github.com/carlossg/docker-maven/blob/master/jdk-7-alpine/Dockerfile#L5-L21
ARG MAVEN_VERSION=3.5.2
ARG USER_HOME_DIR="/root"
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries

RUN mkdir -p /opt/maven /opt/maven/ref && \
    curl -fsSL -o /tmp/apache-maven.tar.gz ${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
    tar -xzf /tmp/apache-maven.tar.gz -C /opt/maven --strip-components=1 && \
    rm -f /tmp/apache-maven.tar.gz && \
    ln -s /opt/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME=/opt/maven \
    MAVEN_CONFIG="$USER_HOME_DIR/.m2"