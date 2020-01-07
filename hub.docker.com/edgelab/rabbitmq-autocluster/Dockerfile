FROM rabbitmq:3.6.15-management-alpine

RUN apk --update add --no-cache curl wget ca-certificates

# Install consul-template
ENV CONSUL_TEMPLATE_VERSION 0.18.1
ENV CONSUL_TEMPLATE_SHA256 72eb9ee8d06f5f02daf4ab5402fdeb466c1f714021a66f28b6e8ec9ff074b7d5

RUN wget -q -O /tmp/consul-template.tgz https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.tgz \
    && echo `sha256sum /tmp/consul-template.tgz` \
    && echo "${CONSUL_TEMPLATE_SHA256} /tmp/consul-template.tgz" \
    && echo "${CONSUL_TEMPLATE_SHA256}  /tmp/consul-template.tgz" | sha256sum -c - \ 
    && tar zxf /tmp/consul-template.tgz -C /usr/local/bin \
    && chmod +x /usr/local/bin/consul-template \
    && rm /tmp/consul-template.tgz

# Version of RabbitMQ to install
ENV PLUGIN_BASE=v3.6.x
ENV AUTOCLUSTER_VERSION=0.10.0
ENV DELAYED_MESSAGE_VERSION=0.0.1


RUN \
  wget -q -O /plugins/rabbitmq_delayed_message_exchange-${DELAYED_MESSAGE_VERSION}.ez  http://www.rabbitmq.com/community-plugins/${PLUGIN_BASE}/rabbitmq_delayed_message_exchange-${DELAYED_MESSAGE_VERSION}.ez && \
  wget -q -O /plugins/autocluster-${AUTOCLUSTER_VERSION}.ez https://github.com/rabbitmq/rabbitmq-autocluster/releases/download/${AUTOCLUSTER_VERSION}/autocluster-${AUTOCLUSTER_VERSION}.ez && \
  wget -q -O /plugins/rabbitmq_aws-${AUTOCLUSTER_VERSION}.ez https://github.com/rabbitmq/rabbitmq-autocluster/releases/download/${AUTOCLUSTER_VERSION}/rabbitmq_aws-${AUTOCLUSTER_VERSION}.ez

# Fetch the external plugins and setup RabbitMQ
RUN \
  rabbitmq-plugins enable --offline \
        autocluster \
        rabbitmq_delayed_message_exchange \
        rabbitmq_top

RUN mkdir /srv/consul
copy consul-wrapper.sh /consul-wrapper.sh

ENTRYPOINT ["/consul-wrapper.sh"]

CMD ["rabbitmq-server"]
