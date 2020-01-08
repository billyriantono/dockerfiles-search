# NFNTY Redis container
# Created: 2017-01-23
# CreatedBy: Jens Walrave
# Last modified: 2017-01-23
# Version 1.0.0

FROM nfntynl/nfnty-runnable:1.0.0
MAINTAINER nfnty

ENV CONTAINER_NAME "nfnty-redis"

ENV RUN_REDIS 1
ENV RUN_REDIS_SUPERVISORD 1
ENV REDIS_PASSWORD ""

RUN apk update && apk add --no-cache redis \
	&& rm -rf /var/cache/apk/*

RUN mkdir -p /etc/redis/
ADD conf/redis.conf /etc/redis/redis.conf
ADD conf/redis-local.conf /etc/redis/redis-local.conf

ADD scripts/start-redis.sh /start-redis.sh
RUN chmod 755 /start-redis.sh

EXPOSE 6379
VOLUME ["/var/lib/redis"]

CMD ["/bin/bash","/start-redis.sh"]