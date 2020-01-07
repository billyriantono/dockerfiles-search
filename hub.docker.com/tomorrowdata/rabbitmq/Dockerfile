FROM rabbitmq:3.6.6-management

COPY rabbitmq-cluster /usr/local/bin/
COPY docker-entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["rabbitmq-cluster"]