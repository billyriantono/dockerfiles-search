FROM ubuntu:precise
MAINTAINER Music Glue "devteam@musicglue.com"

ADD redis.ppa /etc/apt/sources.list.d/redis-server.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C7917B12
RUN apt-get update
RUN apt-get install -y libjemalloc-dev redis-server

EXPOSE 6379
VOLUME ["/var/lib/redis"]
ENTRYPOINT ["/usr/bin/redis-server"]
