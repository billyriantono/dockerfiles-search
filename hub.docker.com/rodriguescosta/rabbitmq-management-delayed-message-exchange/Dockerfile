FROM rabbitmq:3-management
RUN apt-get update && apt-get install wget -y
RUN cd plugins && wget https://github.com/rabbitmq/rabbitmq-delayed-message-exchange/releases/download/v3.8.0/rabbitmq_delayed_message_exchange-3.8.0.ez
RUN rabbitmq-plugins enable rabbitmq_delayed_message_exchange