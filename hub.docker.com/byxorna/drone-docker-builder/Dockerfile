FROM debian
MAINTAINER Gabe Conradi <gummybearx@gmail.com>

ENV DOCKER_HOST unix:///var/run/docker.sock
RUN mkdir /code
WORKDIR /code
RUN apt-get update -y && \
    apt-get install -y curl git && \
    rm -rf /var/lib/apt/lists/*
RUN curl https://get.docker.io/builds/Linux/x86_64/docker-latest -o /usr/local/bin/docker && \
    chmod +x /usr/local/bin/docker 

