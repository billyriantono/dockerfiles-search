# or v0.14-onbuild
FROM fluent/fluentd:v0.14-onbuild

# below RUN includes plugin as examples elasticsearch is not required
# you may customize including plugins as you wish

RUN apk add --update --virtual .build-deps \
        sudo build-base ruby-dev \
 && sudo gem install \
        fluent-plugin-elasticsearch \
 && sudo gem install \
        fluent-plugin-s3 \
 && sudo fluent-gem install \
        fluent-plugin-secure-forward \
 && sudo gem sources --clear-all \
 && apk del .build-deps \
 && rm -rf /var/cache/apk/* \
           /home/fluent/.gem/ruby/2.3.0/cache/*.gem
RUN apk add --update gettext bash curl
RUN mkdir -p /etc/certs
RUN chmod -R 777 /var/log /etc/certs


COPY fluent.conf.template /fluentd/etc/fluent.conf.template
COPY fluent-elastic.conf.template /fluentd/etc/fluent-elastic.conf.template
COPY fluent-s3.conf.template /fluentd/etc/fluent-s3.conf.template
COPY croud_entrypoint.sh /bin/croud_entrypoint.sh
COPY healthcheck.sh /bin/healthcheck.sh

ENV ELASTIC_SEARCH_HOST=elasticsearch
ENV ELASTIC_SEARCH_PORT=9200
ENV FLUSH_INTERVAL=60s

ENTRYPOINT ["/bin/croud_entrypoint.sh"]

HEALTHCHECK --interval=5s --timeout=2s --retries=12 \
  CMD /bin/healthcheck.sh

CMD exec fluentd -c /fluentd/etc/${FLUENTD_CONF} -p /fluentd/plugins $FLUENTD_OPT