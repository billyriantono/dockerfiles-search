FROM rabbitmq:3.6.5

ADD rabbitmq.config /etc/rabbitmq/rabbitmq.config
ADD rabbitmq_auth_backend_http.ez /usr/lib/rabbitmq/lib/rabbitmq_server-3.6.5/plugins/
ADD rabbitmq_topic_authorization.ez /usr/lib/rabbitmq/lib/rabbitmq_server-3.6.5/plugins/

RUN rabbitmq-plugins enable --offline rabbitmq_stomp
RUN rabbitmq-plugins enable --offline rabbitmq_mqtt
RUN rabbitmq-plugins enable --offline rabbitmq_management
RUN rabbitmq-plugins enable --offline rabbitmq_topic_authorization
RUN rabbitmq-plugins enable --offline rabbitmq_auth_backend_http

EXPOSE 15672
EXPOSE 61613
EXPOSE 5672
EXPOSE 1884
