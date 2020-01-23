FROM itdevdixons/ubuntu:14.04

MAINTAINER Viliam Husar viliam.husar@dixonscarphonegroup.com

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y install memcached

EXPOSE 11211

CMD ["/usr/bin/memcached", "-u", "memcache", "-v"]