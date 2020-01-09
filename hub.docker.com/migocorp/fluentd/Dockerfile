FROM fluent/fluentd:v0.12.27
MAINTAINER Larry SU <larrysu1115@gmail.com>

RUN fluent-gem install fluent-plugin-elasticsearch

CMD fluentd -c /fluentd/etc/$FLUENTD_CONF -p /fluentd/plugins $FLUENTD_OPT
