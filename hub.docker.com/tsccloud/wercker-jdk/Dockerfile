# werckerビルド環境: JDK8用
FROM openjdk:8-jdk
MAINTAINER Technosite Cloud
RUN apt-get -y update; \
    apt-get -y upgrade; \
    apt-get -y install \
        apt-utils \
        locales \
        locales-all \
        gawk \
        sudo \
        mysql-client; \
    apt-get clean; \
    apt-get autoclean; \
    apt-get autoremove; \
    sed -i -e "s/^# ja_JP/ja_JP/" /etc/locale.gen; \
    locale-gen; \
    update-locale LANG=ja_JP.UTF-8 LANGUAGE=ja_JP:ja
ENV LANG=ja_JP.UTF-8 LC_ALL=ja_JP.UTF-8 LC_CTYPE=ja_JP.UTF-8
