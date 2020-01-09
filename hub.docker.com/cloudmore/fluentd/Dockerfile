FROM fluent/fluentd:latest-onbuild

EXPOSE 24284

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org'

ARG RUN_DEPS='
ARG BUILD_DEPS='coreutils sudo build-base ruby-dev'

WORKDIR /home/fluent
ENV PATH /home/fluent/.gem/ruby/2.3.0/bin:$PATH

USER root

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
  ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
    && sudo -u fluent gem install fluent-plugin-elasticsearch fluent-plugin-record-reformer fluent-plugin-s3 fluent-plugin-sqs-poll \
    && rm -rf /home/fluent/.gem/ruby/2.3.0/cache/*.gem \
    && sudo -u fluent gem sources -c \
  && apk del $BUILD_DEPS && rm -rf /var/cache/apk/*

USER fluent

CMD exec fluentd -c /fluentd/etc/$FLUENTD_CONF -p /fluentd/plugins $FLUENTD_OPT
