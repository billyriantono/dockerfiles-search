FROM fluent/fluentd:v0.12-onbuild
MAINTAINER Clément BUCHART cbuchart@auchan.fr

RUN apk add --update --virtual .build-deps \
        sudo build-base ruby-dev \
 && sudo gem install \
        fluent-plugin-elasticsearch \
	fluent-plugin-gcloud-pubsub-custom \
 && sudo gem sources --clear-all \
 && apk del .build-deps \
 && rm -rf /var/cache/apk/* \
           /home/fluent/.gem/ruby/2.3.0/cache/*.gem

EXPOSE 24284
