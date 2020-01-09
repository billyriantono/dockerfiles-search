FROM redis

COPY redis.conf /usr/local/etc/redis/redis.conf

VOLUME /var/log/redis
VOLUME /data

USER root

RUN chown -R root:root /var/log

EXPOSE 6379

CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]
