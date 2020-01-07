ARG REDIS_VERSION=5
FROM redis:${REDIS_VERSION}

MAINTAINER <yiane@qq.com>

## For security settings uncomment, make the dir, copy conf, and also start with the conf, to use it
#RUN mkdir -p /usr/local/etc/redis
COPY redis.conf /usr/local/etc/redis/redis.conf
COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

# 在宿主机上执行这句
#RUN echo never > /sys/kernel/mm/transparent_hugepage/enabled;

VOLUME ["/data/redis","/var/log/redis"]

ARG REDIS_AUTH=123456
RUN chmod +x /usr/local/bin/docker-entrypoint.sh \
    && sed -i "s/requirepass foobared/requirepass ${REDIS_AUTH}/" /usr/local/etc/redis/redis.conf

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 6379

CMD ["redis-server", "/usr/local/etc/redis/redis.conf"]
#CMD ["redis-server"]
