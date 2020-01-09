FROM ubuntu:18.04

ENV GHR_VERSION=0.12.0
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get upgrade -y -o Dpkg::Options::="--force-confnew" \
    && apt-get dist-upgrade -y -o Dpkg::Options::="--force-confnew" \
    && apt-get install -y locales \
    && rm -rf /var/lib/apt/lists/*

ENV TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN echo "en_US UTF-8" >/etc/locale.gen
RUN echo "en_US.UTF-8 UTF-8" >>/etc/locale.gen
RUN locale-gen

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV LOG_LEVEL info

RUN apt-get update \
    && apt-get install -y openjdk-8-jdk openjdk-8-jre curl unzip maven openssh-client python3-pip git \
    && apt-get remove --purge -y openjdk-11-jre-headless \
    && pip3 install mkdocs \
    && curl -L -o ghr.tar.gz https://github.com/tcnksm/ghr/releases/download/v${GHR_VERSION}/ghr_v${GHR_VERSION}_linux_amd64.tar.gz \
    && tar -xvzf ghr.tar.gz \
    && mv ghr_v${GHR_VERSION}_linux_amd64/ghr /usr/local/bin/ghr \
    && chmod +x /usr/local/bin/ghr \
    && rm -rf *.tar.gz *.zip ghr_v${GHR_VERSION}_linux_amd64 \
    && apt-get remove --purge -y curl unzip \
    && apt-get autoremove -y --purge \
    && rm -rf /var/lib/apt/lists/*
