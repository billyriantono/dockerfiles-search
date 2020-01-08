FROM fluent/fluentd:v0.14
MAINTAINER WOHLER Paraita <paraita.wohler@activeeon.com>

RUN apk add --update --virtual .build-deps \
    	sudo build-base ruby-dev \

 # cutomize following instruction as you wish
 && sudo gem install \
    	 fluent-plugin-elasticsearch \

 && sudo gem sources --clear-all \
 && apk del .build-deps \
 && rm -rf /var/cache/apk/* \
           /home/fluent/.gem/ruby/2.3.0/cache/*.gem

EXPOSE 24284
