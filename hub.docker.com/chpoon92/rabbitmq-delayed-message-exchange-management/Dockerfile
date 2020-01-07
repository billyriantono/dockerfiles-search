FROM rabbitmq:3.7.14-management
LABEL Alex Poon
ADD ./plugin/rabbitmq_delayed_message_exchange-20171201-3.7.x.ez $RABBITMQ_HOME/plugins/rabbitmq_delayed_message_exchange-20171201-3.7.x.ez
RUN rabbitmq-plugins enable --offline rabbitmq_delayed_message_exchange
