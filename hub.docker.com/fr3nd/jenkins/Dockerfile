FROM jenkins/jenkins:2.141
MAINTAINER Carles Amigó, fr3nd@fr3nd.net

ENV DOCKER_VERSION 1.8.2

USER root
RUN apt-get update && apt-get install -y \
      rsync \
      && rm -rf /usr/share/doc/* && \
      rm -rf /usr/share/info/* && \
      rm -rf /tmp/* && \
      rm -rf /var/tmp/*

RUN curl -L https://get.docker.com/builds/Linux/x86_64/docker-$DOCKER_VERSION > /usr/bin/docker
RUN chmod +x /usr/bin/docker

USER jenkins
