# ruby
#
# VERSION               0.0.1

FROM      php:latest

MAINTAINER Gen Takahashi "gendosu@gmail.com"

ENV LANG=ja_JP.UTF-8

RUN apt-get update \
&&  apt-get upgrade -y --force-yes \
&&  apt-get install -y --force-yes \
    locales \
    git \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

# defaultのlocaleをja_JP.UTF-8にする
RUN echo "ja_JP.UTF-8 UTF-8" > /etc/locale.gen \
&&  locale-gen \
&&  update-locale LANG=ja_JP.UTF-8

# Timezone変更
RUN if [ -e /etc/localtime ]; then rm /etc/localtime; fi \
&&  ln -s /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
&&  dpkg-reconfigure -f noninteractive tzdata

