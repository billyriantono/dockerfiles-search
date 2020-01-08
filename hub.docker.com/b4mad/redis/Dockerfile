#
# Redis Dockerfile
#
# https://github.com/dockerfile/redis
#

# Pull base image.
FROM debian:7.4

# Install Redis.
RUN \
  cd /tmp && \
  apt-get update && \
  apt-get dist-upgrade -y && \
  apt-get install -y redis-server

# Define mountable directories.
VOLUME ["/data"]

ADD redis.conf.dist /etc/redis/redis.conf

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["redis-server", "/etc/redis/redis.conf"]

# Expose ports.
EXPOSE 6379
