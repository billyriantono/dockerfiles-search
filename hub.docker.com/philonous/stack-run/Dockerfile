# @IMAGE stack-run
# @VERSION 2018-03-29-01

FROM ubuntu:latest

RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -y --no-install-recommends  \
      build-essential \
      ca-certificates \
      curl \
      libicu-dev \
      libpq-dev \
      locales \
      msmtp-mta \
      netbase  \
      netcat \
      xz-utils \
        && \
    rm -rf /var/lib/apt/lists/* && \
    localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8


ENV LANG=en_US.UTF-8
