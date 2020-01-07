FROM rabbitmq:3.7-management-alpine

RUN rabbitmq-plugins enable --offline rabbitmq_mqtt
RUN rabbitmq-plugins enable --offline rabbitmq_web_mqtt

# Fix nodename
RUN echo 'NODENAME=rabbit@localhost' > /etc/rabbitmq/rabbitmq-env.conf

#amqp, management, mqtt, ws
EXPOSE 5672 15672 1883 15675

