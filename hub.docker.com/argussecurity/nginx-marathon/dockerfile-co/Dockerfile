FROM fluent/fluentd:latest
USER fluent
WORKDIR /home/fluent
ENV PATH /home/fluent/.gem/ruby/2.2.0/bin:$PATH
USER root
RUN apk --no-cache --update add \
                            build-base \
                            zlib-dev \
                            ruby-dev \
                            libxslt-dev && \
    gem install nokogiri -- --use-system-libraries && \
    gem install fluent-plugin-ftp && \
    gem install fluent-plugin-elasticsearch && \
    apk del build-base zlib-dev ruby-dev libxslt-dev && \
    rm -rf /tmp/* /var/tmp/* /var/cache/apk/*
USER fluent

ONBUILD COPY fluent.conf /fluentd/etc/
ONBUILD COPY plugins /fluentd/plugins/

EXPOSE 24284
CMD fluentd -c /fluentd/etc/$FLUENTD_CONF -p /fluentd/plugins $FLUENTD_OPT
