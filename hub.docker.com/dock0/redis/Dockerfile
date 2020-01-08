FROM dock0/service
MAINTAINER akerl <me@lesaker.org>
EXPOSE 6379
VOLUME /srv/redis
RUN pacman -S --noconfirm redis
ADD redis.conf /srv/redis/config
RUN mkdir -p /var/lib/redis
ADD run /service/redis/run
