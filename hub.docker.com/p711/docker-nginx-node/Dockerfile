FROM nginx

MAINTAINER Ron Arts <ron.arts@novantum.com>

RUN apt-get update -q && apt-get install -y wget apt-utils && \
    wget https://nginx.org/keys/nginx_signing.key && apt-key add ../nginx_signing.key && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install \
    apt-transport-https \
    ca-certificates \
    curl \
    inotify-tools \
    && apt-get clean -y && \
    rm -rf /var/cache/apt/*

RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D && \
    echo 'deb https://apt.dockerproject.org/repo debian-jessie main' > /etc/apt/sources.list.d/docker.list && \
    apt-get update -q && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y docker-engine && \
    apt-get clean -y && \
    rm -rf /var/cache/apt/*

RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
    echo 'deb https://deb.nodesource.com/node_4.x jessie main' > /etc/apt/sources.list.d/nodesource.list && \
    apt-get update -q && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    nodejs \
    && apt-get clean -y && \
    rm -rf /var/cache/apt/*

RUN npm install -g npm@3.8.9
