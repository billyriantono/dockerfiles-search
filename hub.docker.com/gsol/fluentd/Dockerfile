FROM fluent/fluentd:v1.1.3
RUN apk add --update --no-cache --virtual=.deps alpine-sdk ruby-dev libmaxminddb-dev sudo build-base && \
    apk add --update --no-cache geoip-dev && \
    sudo gem install \
      fluent-plugin-elasticsearch \
      fluent-plugin-geoip \
      fluent-plugin-record-reformer \
      fluent-plugin-resolv-filter \
      fluent-plugin-cloudwatch-logs \
      geoip2_c \
      fluent-plugin-slack \
     --no-rdoc --no-ri && \
    sudo gem sources --clear-all && \
    apk del .deps && \
    rm -rf /var/cache/apk/* /tmp/* /var/tmp/* /usr/lib/ruby/gems/*/cache/*.gem
