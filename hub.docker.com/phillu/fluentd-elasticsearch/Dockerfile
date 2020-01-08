FROM fluent/fluentd:v1.3
MAINTAINER Phil Stelzer <phil@philstelzer.com>

RUN apk add --no-cache tzdata
RUN apk add --update --no-cache --virtual .build-deps \
        sudo build-base ruby-dev  \
 && sudo gem install fluent-plugin-elasticsearch \
 && sudo gem sources --clear-all \
 && apk del .build-deps \
 && rm -rf /home/fluent/.gem/ruby/2.3.0/cache/*.gem
