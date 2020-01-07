FROM redis:3.2-alpine
MAINTAINER Santha Kumar <santha.kumar@industrie.co>

RUN apk update && apk upgrade && apk add --update \
        curl \
        bash \
        sed

ENV REDIS_PORT 6379
ENV SENTINEL_PORT 26379
ENV SENTINEL_QUORUM 2
ENV SENTINEL_DOWN_AFTER 5000
ENV SENTINEL_FAILOVER 10000

ADD sentinel.conf /etc/redis/sentinel.conf

EXPOSE $SENTINEL_PORT

COPY entrypoint.sh /entrypoint.sh

RUN chmod 777 /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]