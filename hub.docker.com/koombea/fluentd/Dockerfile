FROM fluent/fluentd:v0.12-onbuild
MAINTAINER Juan Pablo Jaramillo <juan.jaramillo@koombea.com>

RUN apk add --update --virtual .build-deps sudo build-base ruby-dev && \
    sudo gem install fluent-plugin-elasticsearch && \
    sudo gem sources --clear-all && \
    apk del .build-deps && \
    rm -rf /var/cache/apk/* /home/fluent/.gem/ruby/2.3.0/cache/*.gem
    # /usr/lib/ruby/gems/2.3.0/cache

EXPOSE 24224
