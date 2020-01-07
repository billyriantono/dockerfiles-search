FROM rabbitmq:alpine

EXPOSE 5671 5672 15671 15672

RUN rabbitmq-plugins enable --offline rabbitmq_management \
 && rabbitmq-plugins enable --offline rabbitmq_auth_mechanism_ssl \
 && sed -i 's|"{ tcp_listeners, $(rabbit_array) }"|"{ tcp_listeners, $(rabbit_array 5672) }"|' /usr/local/bin/docker-entrypoint.sh \
 && sed -i 's|rabbitConfig=(|rabbitConfig=("{ssl_cert_login_from,common_name}" "$RABBITMQ_EXTRA_CFG"|' /usr/local/bin/docker-entrypoint.sh
