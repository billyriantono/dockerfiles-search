FROM ubuntu:bionic

RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt bionic main restricted universe multiverse" > /tmp/sources.list \
  && echo "deb mirror://mirrors.ubuntu.com/mirrors.txt bionic-updates main restricted universe multiverse" >> /tmp/sources.list \
  && echo "deb mirror://mirrors.ubuntu.com/mirrors.txt bionic-backports main restricted universe multiverse" >> /tmp/sources.list \
  && echo "deb mirror://mirrors.ubuntu.com/mirrors.txt bionic-security main restricted universe multiverse" >> /tmp/sources.list \
  && echo "$(cat /etc/apt/sources.list)" >> /tmp/sources.list \
  && mv /tmp/sources.list /etc/apt/sources.list \
  && apt-get update \
  && apt-get upgrade -y \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /var/cache/apt/* \
  && rm -rf /var/log/*
