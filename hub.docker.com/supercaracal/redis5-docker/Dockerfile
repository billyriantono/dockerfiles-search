FROM debian:jessie-slim

MAINTAINER Taishi Kasuga

RUN apt-get update; \
    apt-get install -y --no-install-recommends wget gcc make libc6-dev ca-certificates; \
    rm -rf /var/lib/apt/lists/*; \
    wget -O redis.tar.gz https://github.com/antirez/redis/archive/5.0-rc3.tar.gz; \
    mkdir -p /usr/src/redis; \
    tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1; \
    rm redis.tar.gz; \
    make -C /usr/src/redis; \
    make -C /usr/src/redis install; \
    rm -r /usr/src/redis; \
    apt-get purge -y --auto-remove wget gcc make libc6-dev ca-certificates

EXPOSE 6379
CMD ["redis-server", "--bind", "0.0.0.0", "--protected-mode", "no", "--daemonize", "no", "--supervised", "no", "--maxmemory", "64mb", "--maxmemory-policy", "allkeys-lru"]
