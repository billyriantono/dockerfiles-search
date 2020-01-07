FROM alpine:3.5

ARG RABBITMQ_VERSION=3.6.9
ARG RABBITMQ_VERSION_TAG=v3_6_9
ARG RABBITMQ_PLUGIN_AUTOCLUSTER_VERSION=0.6.1
ARG ERLANG_VERSION=19.1.0-r0

ENV RABBITMQ_HOME=/rabbitmq_server-${RABBITMQ_VERSION}

ENV PATH=$PATH:${RABBITMQ_HOME}/sbin

RUN echo "--- Install system requirements ---" \
    && apk add --update --no-cache \
      curl \
      xz \
      python \
      erlang=${ERLANG_VERSION} \
      erlang-mnesia=${ERLANG_VERSION} \
      erlang-public-key=${ERLANG_VERSION} \
      erlang-crypto=${ERLANG_VERSION} \
      erlang-ssl=${ERLANG_VERSION} \
      erlang-sasl=${ERLANG_VERSION} \
      erlang-asn1=${ERLANG_VERSION} \
      erlang-inets=${ERLANG_VERSION} \
      erlang-os-mon=${ERLANG_VERSION} \
      erlang-xmerl=${ERLANG_VERSION} \
      erlang-eldap=${ERLANG_VERSION} \
      erlang-syntax-tools=${ERLANG_VERSION} \
    && echo "--- Install RabbitMQ ---" \
    && curl -L https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_${RABBITMQ_VERSION_TAG}/rabbitmq-server-generic-unix-${RABBITMQ_VERSION}.tar.xz | tar xJ \
    && echo "--- Install RabbitMQ plugins ---" \
    && curl -L https://github.com/aweber/rabbitmq-autocluster/releases/download/${RABBITMQ_PLUGIN_AUTOCLUSTER_VERSION}/autocluster-${RABBITMQ_PLUGIN_AUTOCLUSTER_VERSION}.tgz | tar xz -C ${RABBITMQ_HOME} \
    && rabbitmq-plugins enable --offline rabbitmq_management autocluster \
    && echo "--- Install rabbitmqadmin tool ---" \
    && curl -L https://raw.githubusercontent.com/rabbitmq/rabbitmq-management/rabbitmq_${RABBITMQ_VERSION_TAG}/bin/rabbitmqadmin > /usr/bin/rabbitmqadmin \
    && chmod +x /usr/bin/rabbitmqadmin

ENTRYPOINT ["rabbitmq-server"]
