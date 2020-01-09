FROM fluent/fluentd-kubernetes-daemonset:elasticsearch
MAINTAINER EE
WORKDIR /home/fluent
ENV PATH /home/fluent/.gem/ruby/2.2.0/bin:$PATH
RUN apk update
RUN apk upgrade
RUN apk add --update --virtual .build-deps sudo build-base ruby-dev geoip-dev
RUN sudo fluent-gem install fluent-plugin-multi-format-parser
RUN sudo fluent-gem install fluent-plugin-geoip
RUN rm -rf /var/lib/apt/lists/* /home/fluent/.gem/ruby/2.3.0/cache/*.gem
ENV FLUENTD_OPT=""
ENV FLUENTD_CONF="fluent.conf"
EXPOSE 24284
CMD fluentd -c /fluentd/etc/$FLUENTD_CONF -p /fluentd/plugins $FLUENTD_OPT