FROM rabbitmq:3.7-alpine
RUN apk update && apk add --no-cache wget curl unzip
RUN curl -o delayed_message_exchange.zip https://dl.bintray.com/rabbitmq/community-plugins/3.7.x/rabbitmq_delayed_message_exchange/rabbitmq_delayed_message_exchange-20171201-3.7.x.zip
RUN unzip delayed_message_exchange.zip -d $RABBITMQ_HOME/plugins/
RUN rabbitmq-plugins enable --offline rabbitmq_delayed_message_exchange
