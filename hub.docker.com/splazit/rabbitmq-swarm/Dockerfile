FROM rabbitmq:3.7-management-alpine
ADD rabbitmq.conf /etc/rabbitmq/rabbitmq.conf
RUN rabbitmq-plugins enable --offline rabbitmq_peer_discovery_etcd