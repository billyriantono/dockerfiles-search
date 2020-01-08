FROM ubuntu
MAINTAINER apribase

# apt
ADD etc/apt/apt.conf.d/local /etc/apt/apt.conf.d/local
RUN apt-get update
ENV DEBIAN_FRONTEND noninteractive

# wget
RUN apt-get install -y wget ca-certificates

# locale
RUN apt-get install -y language-pack-ja
RUN /usr/sbin/update-locale LANG=ja_JP.UTF-8

# timezone
ADD etc/timezone /etc/timezone
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# clean
RUN apt-get clean
