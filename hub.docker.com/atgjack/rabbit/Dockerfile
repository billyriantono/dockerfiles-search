FROM alpine:latest
MAINTAINER atgJack, https://github.com/atgJack/docker-alpine

# Set environment variables
ENV RABBITMQ_VERSION=3.6.1 \
  RABBITMQ_AUTOCLUSTER_PLUGIN_VERSION=0.4.1 \
  RABBITMQ_AUTOCLUSTER_URL=https://github.com/aweber/rabbitmq-autocluster/releases/download/${RABBITMQ_AUTOCLUSTER_PLUGIN_VERSION}/autocluster-${RABBITMQ_AUTOCLUSTER_PLUGIN_VERSION}.ez \
  PKG_NAME=rabbitmq \
  RABBITMQ_HOME=/opt/rabbitmq \
  RABBITMQ_MNESIA_BASE=/var/lib/rabbitmq 
ENV RABBITMQ_URL=https://www.rabbitmq.com/releases/rabbitmq-server/v${RABBITMQ_VERSION}/rabbitmq-server-generic-unix-${RABBITMQ_VERSION}.tar.xz \
  PATH=${PATH}:${RABBITMQ_HOME}/sbin \
  RABBITMQ_ENABLED_PLUGINS_FILE=${RABBITMQ_HOME}/etc/rabbitmq/enabled_plugins

# Copy Files
# COPY ssl.config ${RABBITMQ_HOME}/etc/rabbitmq/
# COPY standard.config /srv/rabbitmq_server-${RABBITMQMQ_VERSION}/etc/rabbitmq/
# COPY wrapper.sh /usr/bin/wrapper

# Download RabbitMQ
# RUN chmod a+x /usr/bin/wrapper && 

RUN apk add --update curl tar xz bash && \
  echo "http://dl-4.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories && \
  echo "http://dl-4.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
  echo "http://dl-4.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
  apk add erlang erlang erlang-mnesia erlang-public-key erlang-crypto erlang-ssl \
    erlang-sasl erlang-asn1 erlang-inets erlang-os-mon erlang-xmerl erlang-eldap \
    erlang-syntax-tools --update-cache --allow-untrusted && \
  mkdir -p ${RABBITMQ_HOME} && \
  curl -o /opt/${PKG_NAME}.tar.xz ${RABBITMQ_URL} && \
  tar -xf /opt/${PKG_NAME}.tar.xz --strip-components=1 -C ${RABBITMQ_HOME} && \
  rm -f /opt/${PKG_NAME}.tar.xz && \
  touch ${RABBITMQ_ENABLED_PLUGINS_FILE} && \
  curl -L -o ${RABBITMQ_HOME}/plugins/autocluster-${RABBITMQ_AUTOCLUSTER_PLUGIN_VERSION}.ez ${RABBITMQ_AUTOCLUSTER_URL} && \
  rabbitmq-plugins enable --offline rabbitmq_management && \
#  rabbitmq-plugins enable --offline autocluster && \
  apk del --purge tar xz && rm -Rf /var/cache/apk/* && \
  ln -sf ${RABBITMQ_HOME} /rabbitmq

# Expose
EXPOSE      5671/tcp 5672/tcp 15672/tcp 15671/tcp
VOLUME      /var/lib/rabbitmq
CMD         ["rabbitmq-server"]
