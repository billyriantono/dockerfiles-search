FROM ubuntu:16.04
MAINTAINER FBLGIT@GitHub
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -qy redis-server inetutils-ping inetutils-telnet net-tools supervisor
COPY watch-redis.conf /etc/supervisor/conf.d/redis.conf
COPY watch-sentinel.conf /etc/supervisor/conf.d/sentinel.conf
CMD ["/usr/bin/supervisord", "-n"]
