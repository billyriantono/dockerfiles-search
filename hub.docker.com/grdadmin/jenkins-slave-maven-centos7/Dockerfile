FROM openshift/jenkins-slave-maven-centos7

USER root

ENV DOCKER_VERSION 1.12.6

# Install Docker binary
RUN curl -fsSLO https://get.docker.com/builds/Linux/x86_64/docker-${DOCKER_VERSION}.tgz && tar --strip-components=1 -xvzf docker-${DOCKER_VERSION}.tgz -C /usr/bin
