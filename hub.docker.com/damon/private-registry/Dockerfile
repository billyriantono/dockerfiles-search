# damon/registry
# version: 0.1
# run: docker run --name REGISTRY \
#                 -p 5000:5000 \
#                 -h registry \
#                 -e SECRET_KEY='your 64 char key' \
#                 -e SETTINGS_FLAVOR=dev \
#                 damon/registry
FROM registry

RUN DEBIAN_FRONTEND=noninteractive apt-get install -qq supervisor redis-server
RUN mkdir -p /var/log/supervisor

ADD registry_config.yml /docker-registry/config/config.yml
ADD supervisord.conf /etc/supervisor/supervisord.conf
ADD redis.conf /etc/redis.conf

ENV CACHE_REDIS_HOST 127.0.0.1
ENV CACHE_REDIS_PORT 6379
ENV CACHE_REDIS_PASSWORD docker
ENV CACHE_LRU_REDIS_HOST 127.0.0.1
ENV CACHE_LRU_REDIS_PORT 6379
ENV CACHE_LRU_REDIS_PASSWORD docker

# Be sure to add your public keys to /keys/authorized_keys
VOLUME ["/var/log"]
EXPOSE 5000
CMD ["/usr/bin/supervisord"]
