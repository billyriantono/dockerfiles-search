FROM fluent/fluentd:edge
LABEL Description="Listern logstash messages on UDP port and send them into elasticsearch" Vendor="512k"

ENV FLUENTD_PLUGIN_VERSION="3.5.5"

USER root

COPY ./fluent.conf /fluentd/etc/fluent.conf

RUN set -xe \
  && gem install fluent-plugin-elasticsearch --no-rdoc --no-ri --version ${FLUENTD_PLUGIN_VERSION} \
  && fluentd --version

EXPOSE 5160/udp

USER fluent
