FROM fluent/fluentd:v0.14.8
MAINTAINER Michel Vacher <vacher.michel@gmail.com>
USER fluent
WORKDIR /home/fluent
RUN gem install fluent-plugin-elasticsearch
EXPOSE 24284
CMD fluentd -c /fluentd/etc/$FLUENTD_CONF -p /fluentd/plugins $FLUENTD_OPT