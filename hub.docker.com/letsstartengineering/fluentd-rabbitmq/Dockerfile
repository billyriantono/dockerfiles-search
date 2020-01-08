FROM fluent/fluentd:stable
MAINTAINER Lets Start Engineering <info@letsstartengineering.com>

RUN apk add --update --virtual .build-deps \
        sudo build-base ruby-dev \
 && sudo gem install \
        fluent-plugin-rabbitmq \
 && sudo gem sources --clear-all \
 && apk del .build-deps \
 && rm -rf /var/cache/apk/* \
           /home/fluent/.gem/ruby/2.5.0/cache/*.gem

EXPOSE 5140
