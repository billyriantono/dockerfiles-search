FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive
ENV LANG ja_JP.UTF-8en_US.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8

RUN set -x \
    && : "Set Japan locale and time zone." \
    && sed -i.bak -e "s%http://[^ ]\+%http://ftp.jaist.ac.jp/pub/Linux/ubuntu/%g" /etc/apt/sources.list \
    && apt -y update \
    && apt -y upgrade \
    && apt -y install language-pack-ja-base language-pack-ja \
    && locale-gen ja_JP.UTF-8

MAINTAINER mggggk

