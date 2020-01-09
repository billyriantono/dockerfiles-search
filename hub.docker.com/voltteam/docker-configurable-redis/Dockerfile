FROM redis
ADD redis.conf.template /etc/redis.conf.template
ADD docker-entrypoint.sh /usr/local/bin/

ENV REDIS_BIND "0.0.0.0"
ENV REDIS_PASSWORD "changeme"
ENV REDIS_DATABASES 1
ENV REDIS_TIMEOUT 0
ENV REDIS_TCP_KEEPALIVE 300

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["redis-server"]
