FROM alpine:3.8

RUN apk add --update \
    bash \
    bind-tools \
    coreutils \
    curl \
    git \
    htop \
    iotop \
    iputils \
    net-tools \
    strace \
    tcpdump \
    tree \
    vim \
    wget \
  && rm -rf /var/cache/apk/*

RUN git clone https://github.com/Thubo/helper-functions /root/.helper/functions
RUN git clone https://github.com/Thubo/helper-aliases.git /root/.helper/aliases

ADD ./home/bashrc /root/.bashrc
ADD ./home/bash_profile /root/.bash_profile
