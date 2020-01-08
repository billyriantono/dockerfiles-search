FROM ubuntu:xenial

# update apt
RUN apt-get update && apt-get upgrade -y

# i docker
RUN apt-get install -yq apt-transport-https ca-certificates curl
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN echo "deb https://apt.dockerproject.org/repo ubuntu-xenial main" > /etc/apt/sources.list.d/docker.list
RUN apt-get update

ENV DOCKER_VERSION "1.12.3-0~xenial"
RUN apt-get install -yq docker-engine=$DOCKER_VERSION

# docker-compose
RUN curl -L https://github.com/docker/compose/releases/download/1.8.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

# clean
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
