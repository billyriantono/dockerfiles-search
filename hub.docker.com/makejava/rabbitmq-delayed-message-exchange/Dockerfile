FROM rabbitmq:3.8.0-management
#添加插件
ADD rabbitmq_delayed_message_exchange-3.8.0.ez $RABBITMQ_HOME/plugins/rabbitmq_delayed_message_exchange-3.8.0.ez
#启用插件
RUN rabbitmq-plugins enable --offline rabbitmq_delayed_message_exchange
