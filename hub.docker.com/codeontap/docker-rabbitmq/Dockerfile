FROM rabbitmq:3.7
RUN rabbitmq-plugins enable --offline rabbitmq_peer_discovery_aws
COPY rabbitmq.conf /etc/rabbitmq/rabbitmq.conf
