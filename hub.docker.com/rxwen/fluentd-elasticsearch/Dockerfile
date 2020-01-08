# https://github.com/fluent/fluentd-docker-image

FROM fluent/fluentd
MAINTAINER Raymond Wen

USER fluent
WORKDIR /home/fluent
ENV PATH /home/fluent/.gem/ruby/2.2.0/bin:$PATH
RUN gem install fluent-plugin-secure-forward fluent-plugin-elasticsearch fluent-plugin-better-timestamp
EXPOSE 24284
CMD fluentd -c /fluentd/etc/$FLUENTD_CONF -p /fluentd/plugins $FLUENTD_OPT
