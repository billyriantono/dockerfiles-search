FROM ubuntu:14.04

MAINTAINER William Song <ksskor@falinux.com>

RUN locale-gen ko_KR.UTF-8
RUN update-locale LANG=ko_KR.UTF-8
RUN dpkg-reconfigure locales

ENV LANG ko_KR.UTF-8
ENV LC_ALL ko_KR.UTF-8

RUN \
    sed -ri 's/\/archive\.ubuntu\.com/\/ftp\.daum\.net/g' /etc/apt/sources.list && \
    apt-get update && \
    apt-get -y install bind9 bind9utils && \
    rm -rf /var/lib/apt/lists/*

ADD files/init.sh /

CMD ["/init.sh"]

WORKDIR /etc/bind
