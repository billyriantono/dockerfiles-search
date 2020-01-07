FROM ubuntu

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get upgrade -y && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
        bzip2 \
        curl \
        dnsutils \
        git \
        httpie \
        inetutils-traceroute \
        iputils-ping \
        nano \
        php-cli \
        php-mbstring \
        php-xml \
        php-zip \
        wget \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
    && apt-get update && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /root/.ssh \
    && echo Host \* >> /root/.ssh/config \
    && echo ServerAliveInterval 30 >> /root/.ssh/config \
    && echo ServerAliveCountMax 2 >> /root/.ssh/config

RUN apt-get update && apt-get install -y apt-transport-https \
    && curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
    && echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list \
    && apt-get update && apt-get install -y kubectl \
    && rm -rf /var/lib/apt/lists/*
