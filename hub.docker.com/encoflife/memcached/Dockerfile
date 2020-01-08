FROM ubuntu:14.04.1
MAINTAINER Dmitry Mozzherin

ENV LAST_FULL_REBUILD 2015-03-04
# Install packages
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install memcached

# memcached public variable

EXPOSE 11211

CMD ["/usr/bin/memcached", "-m", "64000", "-u", "memcache", "-v"]
