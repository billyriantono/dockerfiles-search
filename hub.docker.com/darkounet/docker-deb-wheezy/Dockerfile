# Wheezy Dockerfile
# For dev use only

FROM debian:wheezy

MAINTAINER Antoine GUEVARA <me@antoine-guevara.fr>

ENV HOSTNAME wheezy.docker.lan
ENV DEBIAN_FRONTEND noninteractive
ENV SHELL /bin/bash

RUN apt-get update

RUN apt-get install -y -qq vim htop strace wget

RUN apt-get install -y -qq devscripts

ENTRYPOINT ["/bin/bash"]
