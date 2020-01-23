FROM rabbitmq:3.7.4-management-alpine

LABEL maintainer="Ruzhentsev Alexandr <noc@mirafox.ru>"
LABEL version="1.0"
LABEL description="Docker image Rabbitmq + Management Plugin + Create users script"

ADD docker-entrypoint.sh /docker-entrypoint.sh
ADD create_users.sh /create_users.sh

RUN chmod +x /docker-entrypoint.sh \
    && chmod +x /create_users.sh

CMD ["/docker-entrypoint.sh"]
