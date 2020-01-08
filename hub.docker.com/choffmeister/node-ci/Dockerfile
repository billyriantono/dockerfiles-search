FROM node:12.13.0
MAINTAINER Christian Hoffmeister <mail@choffmeister.de>

ENV NODE_VERSION="12.13.0"
ENV DOCKER_VERSION="17.12.1-ce"

WORKDIR /tmp
RUN \
  wget -q https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz && \
  echo "9dd0d19312640460671352930eb44b1692441d95  docker-$DOCKER_VERSION.tgz" | shasum -c - && \
  tar xf docker-$DOCKER_VERSION.tgz && \
  mv docker /opt/docker && \
  ln -s /opt/docker/docker /usr/bin/docker && \
  rm -r docker-$DOCKER_VERSION.tgz

WORKDIR /root