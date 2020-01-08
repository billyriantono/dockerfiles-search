FROM node:6.3.0
MAINTAINER Huang Rui <vowstar@gmail.com>

ENV LANG="zh_CN.UTF-8" LANGUAGE="en_US:en" LC_ALL="zh_CN.UTF-8" NPM_CONFIG_LOGLEVEL=info

RUN echo "deb http://httpredir.debian.org/debian jessie-backports main" > /etc/apt/sources.list.d/backports.list && \
    DEBIAN_FRONTEND=noninteractive apt-get update -qq && \
    DEBIAN_FRONTEND=noninteractive apt-get install -yq \
        locales \
        git \
        openssh-client \
        procps \
        bzip2 \
        graphviz \
        fonts-noto \
        fonts-noto-cjk \
        fonts-wqy-microhei \
        locales-all \
        python \
        calibre \
        openjdk-7-jre-headless && \
    locale-gen && \
    echo "zh_CN.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "zh_CN GB2312" >> /etc/locale.gen && \
    echo "zh_CN.GB18030 GB18030" >> /etc/locale.gen && \
    echo "zh_CN.GBK GBK" >> /etc/locale.gen && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    echo 'LANG="zh_CN.UTF-8 UTF-8"'>/etc/default/locale && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=zh_CN.UTF-8 && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    npm install -d gitbook-cli svgexport -g && \
    gitbook -V && \
    npm cache clean && \
    rm -rf /tmp/npm* /tmp/tmp* && \
    DEBIAN_FRONTEND=noninteractive apt-get purge -yq \
        -h &&\
    DEBIAN_FRONTEND=noninteractive apt-get autoremove -yq --purge && \
    DEBIAN_FRONTEND=noninteractive apt-get clean && \
    rm -rf /tmp/*

EXPOSE 4000
