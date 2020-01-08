FROM       ubuntu:15.04
MAINTAINER Carlos José Vaz <carlosjvaz@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# update repository
RUN echo "deb http://archive.ubuntu.com/ubuntu vivid main universe" > /etc/apt/sources.list
RUN apt-get update && \
    apt-get dist-upgrade -y

# install utils programs
RUN apt-get -y -qq install --no-install-recommends \
                           git-core zip bzip2 curl wget unzip

# prepare locales
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "pt_BR.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen --purge --lang en_US \
    && locale-gen --purge --lang pt_BR \
    && locale-gen

# clean
RUN apt-get autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*  /var/cache/apt/*
