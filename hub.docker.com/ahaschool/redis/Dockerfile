FROM redis:latest
COPY redis.conf /usr/local/etc/redis/redis.conf
VOLUME ["/usr/local/etc/redis"]
CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]
