FROM rabbitmq:3.7.6-alpine

LABEL maintainer="Artem Egorkine" \
      description="PIM rabbimq image" \
      version="3.7-alpine"

RUN mkdir -p /var/run/rabbitmq \
 && chown rabbitmq:rabbitmq /var/run/rabbitmq \
 && chmod 2770 /var/run/rabbitmq

RUN mkdir -p /var/lib/rabbitmq/conf.d \
 && chown rabbitmq:rabbitmq /var/lib/rabbitmq/conf.d \
 && chmod 777 /var/lib/rabbitmq/conf.d

ENV RABBITMQ_PID_FILE /var/run/rabbitmq/rabbitmq.pid
ENV RMQCONF /var/lib/rabbitmq/conf.d

COPY pim-docker-entrypoint.sh /usr/local/bin/
COPY rmq-post-startup-tune.sh /usr/local/bin/

ENTRYPOINT ["pim-docker-entrypoint.sh"]
CMD [ "docker-entrypoint.sh", "rabbitmq-server" ]
