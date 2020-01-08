FROM redis:3-alpine

RUN apk add --update --no-cache bash

COPY redis.conf /etc/redis.conf
COPY sentinel.conf /etc/sentinel.conf
COPY docker-entrypoint.sh /root/docker-entrypoint.sh

RUN chown redis:redis /etc/sentinel.conf

ENTRYPOINT ["/root/docker-entrypoint.sh"]
CMD ["redis"]