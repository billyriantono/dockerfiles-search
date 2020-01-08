FROM alpine:3.10
MAINTAINER Perficient-DevOps

RUN apk --no-cache add \
    bash \
    curl \
    docker \
    git \
    openjdk8-jre && \
    mkdir -p /var/lib/jenkins

# Install Jenkins slave jar
ARG JENKINS_REMOTING_VERSION=3.27
# See https://github.com/jenkinsci/docker-slave/blob/master/Dockerfile#L31
RUN curl --create-dirs -sSLo /usr/share/jenkins/slave.jar https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/$JENKINS_REMOTING_VERSION/remoting-$JENKINS_REMOTING_VERSION.jar \
  && chmod 755 /usr/share/jenkins \
  && chmod 644 /usr/share/jenkins/slave.jar

COPY bin/entrypoint.sh /entrypoint.sh

WORKDIR /var/lib/jenkins

ENTRYPOINT ["/entrypoint.sh"]
