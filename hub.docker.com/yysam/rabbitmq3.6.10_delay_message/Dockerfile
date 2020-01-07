# rabbitmq
#
# docker build -t myrabbitmq -f Dockerfile.rabbit .
# docker run -d -p 5672:5672 -p 15672:15672 --name myrabbitmq -e RABBITMQ_DEFAULT_USER=user -e RABBITMQ_DEFAULT_PASS=password myrabbitmq


FROM rabbitmq:3.6.10-management-alpine

COPY rabbitmq_delayed_message_exchange-0.0.1.ez  $RABBITMQ_HOME/plugins/rabbitmq_delayed_message_exchange-0.0.1.ez

RUN rabbitmq-plugins enable --offline rabbitmq_delayed_message_exchange
