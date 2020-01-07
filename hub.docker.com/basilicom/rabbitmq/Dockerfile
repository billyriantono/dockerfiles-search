FROM rabbitmq

RUN rabbitmq-plugins enable --offline rabbitmq_management
RUN rabbitmq-plugins enable --offline rabbitmq_stomp
RUN rabbitmq-plugins enable --offline rabbitmq_web_stomp

COPY docker-entrypoint-monitoring.sh /usr/local/bin/
RUN ln -s usr/local/bin/docker-entrypoint-monitoring.sh / # backwards compat

EXPOSE 15671 15672 15674 61613

ENTRYPOINT ["docker-entrypoint-monitoring.sh"]


