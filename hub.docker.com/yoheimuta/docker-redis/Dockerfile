FROM ubuntu:14.04
MAINTAINER Yohei Yoshimuta "yoheimuta@gmail.com"
ENV REFRESHED_AT 2014-09-16
RUN apt-get update
RUN apt-get -y install redis-server redis-tools
EXPOSE 6379
ENTRYPOINT [ "/usr/bin/redis-server" ]
CMD []
