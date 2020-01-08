# Set the base image to redis
FROM redis:3.0.5

# File Author / Maintainer
MAINTAINER tomiti

COPY ./redis.conf /usr/local/etc/redis/redis.conf
CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]
