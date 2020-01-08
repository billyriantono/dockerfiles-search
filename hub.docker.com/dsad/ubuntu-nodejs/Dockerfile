FROM ubuntu:14.04

RUN sed -e 's/^# deb /deb /g' /etc/apt/sources.list | grep "^deb " > /etc/apt/sources.list.new && \
    mv /etc/apt/sources.list.new /etc/apt/sources.list && \
    export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -y \
      openssl \
      ca-certificates \
      rsyslog \
      rsyslog-relp \
      cron \
      curl \
      rsync \
      logrotate  \
      gettext-base \
      wget \
      less \
      bash \
      bash-completion \
      tar \
      zip \
      unzip \
      git \
      emacs24-nox \
      jq figlet \
      build-essential \
      python \
      vim && \ 
      apt-get clean && \
      rm -rf /var/lib/apt/lists/*

RUN wget -qO- https://deb.nodesource.com/setup_4.x | bash - && \
    export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -y nodejs && \ 
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip"
RUN unzip awscli-bundle.zip
RUN ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws

ADD rootfs /