FROM jenkins/jenkins:lts
MAINTAINER Brian Bassett <bbassett1276@gmail.com>

ENV DOCKER_VERSION 17.12.1
USER root
RUN mkdir /tmp/unpack && cd /tmp/unpack \
    && wget https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}-ce.tgz \
    && tar xfvz docker-${DOCKER_VERSION}-ce.tgz  \
    && mv docker/docker /usr/bin \
    && chmod u+s /usr/bin/docker \
    && cd / && rm -rf /tmp/unpack
USER jenkins

