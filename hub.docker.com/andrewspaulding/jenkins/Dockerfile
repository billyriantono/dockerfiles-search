FROM jenkins/jenkins:lts-alpine

USER root

ARG MAVEN_VERSION=3.6.3
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries

#install maven
RUN mkdir -p /usr/share/maven /usr/share/maven/ref \
  && curl -fsSL -o /tmp/apache-maven.tar.gz ${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
  && tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 \
  && rm -f /tmp/apache-maven.tar.gz \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

#install aws cli
RUN apk update \
  && apk add python \
  && cd /tmp \
  && curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip" \
  && unzip awscli-bundle.zip \
  && ./awscli-bundle/install -i /usr/share/aws -b /usr/bin/aws \
  && rm awscli-bundle.zip \
  && rm -r awscli-bundle

#install docker in docker
RUN apk add docker

USER jenkins

ENV M2_HOME /usr/share/maven

ENV M2 ${M2_HOME}/bin

ENV PATH ${PATH}:${M2_HOME}:${M2}