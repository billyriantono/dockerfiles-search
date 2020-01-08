FROM debian:jessie

MAINTAINER stuart nixon <dotcomstu@gmail.com>
ENV DEBIAN_FRONTEND noninteractive

RUN \
  apt-get update \
  && apt-get install -y wget docker.io build-essential tcl ruby2.0 bundler

RUN \
  wget -q -O - 'http://github.com/antirez/redis/archive/3.0.0-rc1.tar.gz' | tar -xzvf - -C /opt \
  && mv /opt/redis-3.0.0-rc1 /opt/redis \
  && cd /opt/redis

RUN \
  cd /opt/redis \
  && make V=1 \
#  && make test \
  && make install \
  && mkdir -p /usr/local/etc/redis/ \
  && cp redis.conf /usr/local/etc/redis/redis.conf

RUN \
  cp /opt/redis/src/redis-trib.rb /usr/local/bin \
  && gem install redis

EXPOSE 6379



CMD [ "/usr/local/bin/redis-server", "/usr/local/etc/redis/redis.conf" ]

ADD ./redis.conf /usr/local/etc/redis/redis.conf


