FROM ubuntu:16.04

ARG DOCKER_VERSION=1.13.0-rc4

RUN apt-get update \
 && apt-get install -y wget make \
 && wget -qO - https://test.docker.com/builds/Linux/x86_64/docker-${DOCKER_VERSION}.tgz |tar xfz - -C /usr/bin/ --strip-components=1
