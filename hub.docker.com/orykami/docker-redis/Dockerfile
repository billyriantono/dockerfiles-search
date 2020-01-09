# Redis Dockerfile
# https://github.com/orykami/docker-redis
FROM redis:alpine
# Copying default Redis configuration file onto container
COPY config/redis.conf /usr/local/etc/redis/redis.conf
# Running redis-server with our custom configuration file
CMD [ "redis-server", "/usr/local/etc/redis/redis.conf" ]