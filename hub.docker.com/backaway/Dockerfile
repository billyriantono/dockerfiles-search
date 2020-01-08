# Version 1.0.0
FROM ubuntu:14.04
MAINTAINER Wang Huizhou "whz.job@gmail.com"
ENV REFRESHED_AT 2015-10-24

RUN apt-get update
RUN apt-get -y install redis-server redis-tools

EXPOSE 6379

ENTRYPOINT ["/usr/bin/redis-server"]
CMD []
