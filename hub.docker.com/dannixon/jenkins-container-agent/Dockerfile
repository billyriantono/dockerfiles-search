FROM lsiobase/ubuntu:bionic

# Install Java and Docker
RUN apt-get update && \
    apt-get install -y \
      apt-transport-https \
      ca-certificates \
      curl \
      software-properties-common \
      openjdk-8-jdk && \
    curl -fsSL 'https://download.docker.com/linux/ubuntu/gpg' | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce

ARG JENKINS_SLAVE_VERSION=3.26

# Setup Jenkins slave
RUN curl --create-dirs -sSLo '/usr/share/jenkins/slave.jar' \
      "https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/${JENKINS_SLAVE_VERSION}/remoting-${JENKINS_SLAVE_VERSION}.jar" && \
    chmod 755 '/usr/share/jenkins' && \
    chmod 644 '/usr/share/jenkins/slave.jar'
ENV JENKINS_AGENT_WORKDIR=/config

COPY root/ /
