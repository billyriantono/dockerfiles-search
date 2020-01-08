FROM ubuntu:16.04
LABEL maintainer "UshioShugo<ushio.s@gmail.com>"

ENV DOCKER_VER=17.03.1-ce \
    DOCKER_COMPOSE_VER=1.13.0

RUN apt-get -qq update && \
    apt-get install -y curl  build-essential

RUN set -x && \
    curl -L -o /tmp/docker-${DOCKER_VER}.tgz https://get.docker.com/builds/Linux/x86_64/docker-${DOCKER_VER}.tgz && \
    tar -xz -C /tmp -f /tmp/docker-${DOCKER_VER}.tgz && \
    mv /tmp/docker/* /usr/bin

RUN curl -L https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VER}/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose
