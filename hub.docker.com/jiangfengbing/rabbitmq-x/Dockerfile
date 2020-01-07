FROM rabbitmq:3.7-management

ADD *.ez /opt/rabbitmq/plugins/

RUN rabbitmq-plugins enable rabbitmq_delayed_message_exchange \
  && rabbitmq-plugins enable rabbitmq_management_exchange \
  && rabbitmq-plugins enable prometheus_rabbitmq_exporter \
  && rabbitmq-plugins enable prometheus_process_collector \
  && apt-get update && apt-get install -y wget

