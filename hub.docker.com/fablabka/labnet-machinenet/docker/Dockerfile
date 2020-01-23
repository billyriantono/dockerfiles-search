FROM redis:3.2
LABEL maintainer="fabianmu <spam@fabian.mu>"

COPY redis.conf /usr/local/etc/redis/redis.conf
CMD [ "redis-server", "/usr/local/etc/redis/redis.conf", "--appendonly", "yes"]