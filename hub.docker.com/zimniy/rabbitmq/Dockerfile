FROM rabbitmq:management
MAINTAINER zimniy@cyberbrain.pw

ENV RABBITMQ_USE_LONGNAME="true" \
    RABBITMQ_LOGS="-" \
    RABBITMQ_SSL_CERTFILE="/opt/ssl/cert.pem" \
    RABBITMQ_SSL_KEYFILE="/opt/ssl/privkey.pem" \
    RABBITMQ_SSL_CACERTFILE="/opt/ssl/chain.pem" \
    RABBITMQ_CTL_ERL_ARGS="-proto_dist inet_tls" \
    RABBITMQ_SSL_FAIL_IF_NO_PEER_CERT="false" \
    RABBITMQ_SSL_VERIFY="verify_none"

VOLUME ["/opt/ssl"]

EXPOSE 35197
