FROM ubuntu
MAINTAINER Ian Duncan <ian@iankduncan.com>
RUN echo deb http://ppa.launchpad.net/chris-lea/redis-server/ubuntu precise main >> /etc/apt/sources.list
RUN apt-key adv --keyserver pgp.mit.edu --recv-key B9316A7BC7917B12
RUN apt-get update
RUN apt-get install -y redis-server
EXPOSE 6379
ADD redis.conf /etc/redis/redis.conf
RUN echo 1 > /proc/sys/vm/overcommit_memory
ENTRYPOINT /usr/bin/redis-server /etc/redis/redis.conf
VOLUME ["/var/lib/redis", "/var/log/redis"]
