FROM rabbitmq

# default port 15674
RUN rabbitmq-plugins enable --offline rabbitmq_web_stomp

# default port 15672: access with ssh port forwarding
RUN rabbitmq-plugins enable --offline rabbitmq_management

EXPOSE 15674
