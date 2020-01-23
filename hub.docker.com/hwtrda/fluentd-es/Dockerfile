FROM fluent/fluentd:latest

RUN gem install fluent-plugin-elasticsearch fluent-plugin-s3 --no-rdoc --no-ri

VOLUME ["/fluentd/data"]

USER root

CMD fluentd -c /etc/fluent.conf
