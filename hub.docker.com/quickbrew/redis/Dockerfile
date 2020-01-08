FROM ubuntu:latest
MAINTAINER Simon Menke <simon.menke@gmail.com>

RUN apt-get update
RUN apt-get -yy install redis-server

ADD redis.conf /etc/redis/redis.conf
ADD run.sh /run-redis.sh

EXPOSE 6379

ENTRYPOINT ["bash", "/run-redis.sh"]
