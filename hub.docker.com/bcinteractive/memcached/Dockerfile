FROM gliderlabs/alpine:3.3
MAINTAINER Bruno CHIREZ <contact@brunochirez.com>

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN getent group memcache || addgroup memcache \
    && getent passwd memcache || adduser -D -H -G memcache memcache

ENV MEMCACHE_VERSION 1.4.25
ENV ALPINE_MEMCACHE_VERSION 1.4.25-r0

RUN apk --update add memcached=${ALPINE_MEMCACHE_VERSION} \
    && rm -rf /var/cache/apk/*

EXPOSE 11211

USER memcache
ENTRYPOINT ["memcached"]