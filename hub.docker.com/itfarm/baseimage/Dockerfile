FROM itfarm/baseimage:latest

RUN set -xe && \
    apt-get update && apt-get install -y \
      gettext \
      vim \
      curl \
      wget \
      sudo \
      net-tools \
      ca-certificates \
      unzip \
      apt-transport-https \
      rsync \
      git \
      inetutils-ping \
      tzdata \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
