FROM ubuntu:bionic

RUN apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y language-pack-zh-hant-base language-pack-zh-hant tzdata \
  && apt-get autoremove \
  && apt-get autoclean \
  && apt-get clean \
  && update-locale LANG=zh_TW.UTF-8 LANGUAGE=zh_TW:zh \
  && ln -fs /usr/share/zoneinfo/Asia/Taipei /etc/localtime \
  && dpkg-reconfigure -f noninteractive tzdata \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /var/cache/apt/* \
  && rm -rf /var/log/*

ENV LANG zh_TW.UTF-8
ENV LC_ALL zh_TW.UTF-8
ENV LC_CTYPE zh_TW.UTF-8
