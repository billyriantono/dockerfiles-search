FROM eliumio/docker-jenkins:2.90
MAINTAINER Elium Tech <tech@elium.io>

ENV DOCKER_COMPOSE_VERSION 1.10.1

USER root
# Add docker-compose
RUN apk --update add docker py-pip py-yaml ca-certificates openssl &&\
    pip install -U docker-compose==${DOCKER_COMPOSE_VERSION} &&\
    rm -rf `find / -regex '.*\.py[co]' -or -name apk` &&\
    adduser jenkins docker

USER jenkins
