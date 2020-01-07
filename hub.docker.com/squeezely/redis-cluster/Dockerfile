FROM redis

RUN apt-get update && apt-get install -y supervisor

COPY supervisord.conf /etc/supervisor/supervisord.conf

ENV REDIS_PORT_MASTER 11600
ENV REDIS_PORT_SLAVE 11601

ENV REDIS_CONF_MASTER nodesmaster.conf
ENV REDIS_CONF_SLAVE nodesslave.conf

EXPOSE $REDIS_PORT_MASTER
EXPOSE $REDIS_PORT_SLAVE

COPY entrypoint.sh /usr/local/bin/

COPY redis.conf /usr/local/etc/redismaster.conf
COPY redis.conf /usr/local/etc/redisslave.conf

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
