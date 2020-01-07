FROM ubuntu:14.04
MAINTAINER zsx "zsx0728@163.com"
ENV REFRESHED_AT 2019-11-01

RUN sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list
RUN apt-get update -y && apt-get -y install redis-server redis-tools

EXPOSE 6379
ENTRYPOINT [ "/usr/bin/redis-server" ]
CMD []
