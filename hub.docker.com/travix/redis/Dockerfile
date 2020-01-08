FROM redis:3.2-alpine

MAINTAINER Travix

ENV REDIS_CONFIG_PATH="/opt/redis.conf" \
    SENTINEL_SERVICE_TIMEOUT=20

RUN apk add --update bash \
    && rm -rf /var/cache/apk/*

COPY redis.conf /opt/
COPY docker-entrypoint.sh /usr/local/bin/
