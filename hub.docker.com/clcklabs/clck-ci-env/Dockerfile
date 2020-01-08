# Maven with Java

FROM openjdk:13-jdk-alpine

#FROM adoptopenjdk/openjdk11:alpine-slim
#FROM openjdk:8u191-jdk-alpine

MAINTAINER ClckLabs <info@clcklabs.com>

# Install necessary tools

ARG RANCHER_VER=v2.2.0
ARG MAVEN_VERSION=3.5.4
ARG USER_HOME_DIR="/root"
ARG SHA=2a803f578f341e164f6753e410413d16ab60fabe31dc491d1fe35c984a5cce696bc71f57757d4538fe7738be04065a216f3ebad4ef7e0ce1bb4c51bc36d6be86
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries

RUN apk update \
    && apk add --no-cache curl tar bash xz openssh-client git git-subtree apache-ant python3 py3-pip \
    && ln -s /usr/bin/python3 /usr/bin/python \
    && pip3 install --upgrade pip \
    && pip3 install awscli \
    && curl -o /usr/local/bin/ecs-cli https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest \
    && chmod +x /usr/local/bin/ecs-cli \
    && apk add --update --no-cache nodejs npm \
    && npm install -g n \
    && npm install -g yarn \
    && npm install -g lerna \
    && curl -o /tmp/rancher-cli.tgz https://releases.rancher.com/cli2/${RANCHER_VER}/rancher-linux-amd64-${RANCHER_VER}.tar.gz \
    &&  tar -xf /tmp/rancher-cli.tgz -C /opt/ \
    && ln -s /opt/rancher-${RANCHER_VER}/rancher /usr/local/bin/rancher \
    && rm /tmp/rancher-* \
    && echo "Downloading:  ${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz" \
    && mkdir -p /usr/share/maven /usr/share/maven/ref \
    && curl -fsSL -o /tmp/apache-maven.tar.gz ${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
    && echo "${SHA}  /tmp/apache-maven.tar.gz" | sha512sum -c - \
    && tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 \
    && rm -f /tmp/apache-maven.tar.gz \
    && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"

COPY mvn-entrypoint.sh /usr/local/bin/mvn-entrypoint.sh
COPY settings-docker.xml /usr/share/maven/ref/

RUN chmod +x /usr/local/bin/mvn-entrypoint.sh

VOLUME "$USER_HOME_DIR/.m2"

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["mvn"]
