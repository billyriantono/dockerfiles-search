# Tan Bui Docker Base Image, based on Ubuntu 18.04
# - docker build -t tanbui/ubuntu_base:18.04 .
#
# NOTE: change parameters' values to your own ones
# Create the container:
# - docker run -it -e TZ=Europe/Helsinki --name tanub18 tanbui/ubuntu_base:18.04 /bin/bash
#

FROM ubuntu:18.04
LABEL maintainer="trungtanbui@gmail.com"

ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_CTYPE en_US.UTF-8


RUN DEBIAN_FRONTEND=noninteractive  apt update -y && \
    DEBIAN_FRONTEND=noninteractive  apt upgrade -y

RUN DEBIAN_FRONTEND=noninteractive  apt -y install software-properties-common vim wget curl && \
    DEBIAN_FRONTEND=noninteractive  apt -y install locales language-pack-en-base tzdata htop

# fix user environment
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN locale-gen en_US.UTF-8