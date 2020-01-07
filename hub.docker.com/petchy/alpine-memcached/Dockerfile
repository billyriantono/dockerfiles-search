FROM dearteno/alpine-base
MAINTAINER Pichate Ins <cogent@cogentwebworks.com>

ENV MEMCACHED_MEMORY 128
ENV MEMCACHED_MAX_CONNECTIONS 1024
ENV MEMCACHED_MAX_ITEM_SIZE 4M

RUN apk-install-edge memcached

RUN addgroup -S memcache && \
    adduser -D -S -h /var/cache/memcache -s /sbin/nologin -G memcache memcache

COPY rootfs /

ENTRYPOINT ["/init"]
CMD []

EXPOSE 11211
