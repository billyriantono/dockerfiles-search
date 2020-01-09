FROM ubuntu:14.04

MAINTAINER Andreas Hucks "andreas@inputrequired.org"

RUN \
    apt-get update && \
    apt-get install -y apt-cacher-ng

EXPOSE 3142
VOLUME /var/cache/apt-cacher-ng

CMD \
    chmod 777 /var/cache/apt-cacher-ng && \
    /etc/init.d/apt-cacher-ng start && \
    tail -f /var/log/apt-cacher-ng/*