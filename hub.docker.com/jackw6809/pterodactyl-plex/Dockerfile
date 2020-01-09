FROM ubuntu:18.04

MAINTAINER Jack W, <jack@oxide.host>

RUN apt update \
    && apt upgrade -y \
    && apt autoremove -y \
    && apt -y install curl software-properties-common locales git cmake sudo wget dpkg \
    && useradd -d /home/container -m container

    # Ensure UTF-8
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
