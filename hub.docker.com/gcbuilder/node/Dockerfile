FROM node:lts-buster

RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list && \
  sed -i 's/security.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list && \
  apt-get update -y && \
  apt-get install -y --no-install-recommends \
    openssh-client wget zip unzip git tree gcc \
    g++ build-essential cmake apt-transport-https \
    ca-certificates openssl gettext-base && \
  rm -rf /var/lib/apt/lists/* && \
  yarn global add cnpm npm && \
  mkdir -p ~/.ssh

COPY ./scripts/init_ssh /usr/bin
COPY ./scripts/init_git /usr/bin
COPY ./scripts/init_npm /usr/bin
