FROM fluent/fluentd:v0.14.14

MAINTAINER fengcen <fengcen.love@gmail.com>

USER root

RUN apk add --update --virtual .build-deps \
        sudo build-base ruby-dev \
    && sudo -u fluent gem install \
        fluent-plugin-elasticsearch \
    && sudo -u fluent gem sources --clear-all \
    && apk del .build-deps \
    && rm -rf /var/cache/apk/* \
           /home/fluent/.gem/ruby/2.3.0/cache/*.gem
