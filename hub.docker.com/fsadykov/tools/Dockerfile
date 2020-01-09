FROM centos:7

MAINTAINER Farkhod Sadykov <sadykov.farkhod@gmail.com>

## Version of the docker cli
ENV DOCKERVERSION=18.03.1-ce

## Download docker cli
RUN curl -fsSLO https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKERVERSION}.tgz \
  && tar xzvf docker-${DOCKERVERSION}.tgz --strip 1 -C /usr/local/bin docker/docker \
  && rm docker-${DOCKERVERSION}.tgz

## Install kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.13.0/bin/linux/amd64/kubectl \
    && chmod +x ./kubectl \
    && mv ./kubectl /usr/local/bin/kubectl \
    && mkdir ~/.kube

## Copy Script to set ~/.kube/config
COPY . /scripts/
RUN chmod +x -R /scripts/set-config.sh

## start jenkins on container start
CMD su - root -c "sh /scripts/set-config.sh"
