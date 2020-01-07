# ubuntu-base
#
# VERSION               0.0.1

FROM      ubuntu:16.10

MAINTAINER Gen Takahashi <gendosu@gmail.com>

RUN apt-get update \
&&  apt-get upgrade -y --force-yes \
&& apt-get install -y --force-yes \
  libssl-dev \
  libreadline-dev \
  zlib1g-dev \
  language-pack-ja \
  wget \
  curl \
  git \
  build-essential \
  vim \
&& apt-get clean \
&& rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# defaultのlocaleをja_JP.UTF-8にする
ENV LANG=ja_JP.UTF-8
RUN update-locale LANG=ja_JP.UTF-8

# Timezone変更
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
&&  dpkg-reconfigure -f noninteractive tzdata

