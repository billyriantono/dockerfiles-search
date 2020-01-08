FROM redis:3.2-alpine
MAINTAINER Santha Kumar <santha.kumar@industrie.co>

RUN apk update && apk upgrade && apk add --update \
        curl \
        bash \
        sed

ENV REDIS_PORT 6379
ADD redis.conf /etc/redis/redis.conf
EXPOSE $REDIS_PORT

COPY entrypoint.sh /entrypoint.sh

RUN chmod 777 /entrypoint.sh

ENTRYPOINT [ "/entrypoint.sh" ]