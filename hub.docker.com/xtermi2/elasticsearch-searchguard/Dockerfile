# Instructions to build this image
FROM docker.elastic.co/elasticsearch/elasticsearch-oss:6.6.2

ARG VCS_REF
ARG BUILD_DATE

LABEL description="elasticsearch secured with search-guard"
LABEL org.label-schema.name="elasticsearch-searchguard"
LABEL org.label-schema.description="elasticsearch secured with search-guard"
LABEL org.label-schema.usage="https://github.com/xtermi2/elasticsearch-searchguard/tree/master/example"
LABEL org.label-schema.url="https://github.com/xtermi2/elasticsearch-searchguard"
LABEL org.label-schema.vcs-url="https://github.com/xtermi2/elasticsearch-searchguard"
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.build-date=$BUILD_DATE

ENV ES_VERSION "6.6.2"
ENV SG_VERSION "24.2"
ENV PROMETHEUS_EXPORTER_VERSION "6.6.2.0"

ENV ELASTIC_PWD "changeme"
ENV KIBANA_PWD "changeme"
ENV BEATS_PWD "changeme"
ENV ADMIN_KEY_PASS "changeme"

ENV SG_CONFIG_DIR "/usr/share/elasticsearch/sg_config"
ENV SG_CERT_DIR "/usr/share/elasticsearch/config/certificates"
ENV ROOT_CA "root-ca.pem"
ENV ADMIN_PEM "admin.pem"
ENV ADMIN_KEY "admin.key"

RUN mkdir -p $SG_CONFIG_DIR $SG_CERT_DIR \
    && chmod -R 0775 $SG_CONFIG_DIR $SG_CERT_DIR

COPY --chown=elasticsearch:0 ./src/main/resources/sg_config $SG_CONFIG_DIR
COPY --chown=elasticsearch:0 ./src/main/resources/bin /usr/local/bin

RUN echo "===> Installing search-guard..." \
    && chmod -R +x /usr/local/bin \
    && elasticsearch-plugin install -b "com.floragunn:search-guard-6:$ES_VERSION-$SG_VERSION" \
    && echo "===> Installing elasticsearch-prometheus-exporter..." \
    && elasticsearch-plugin install -b https://distfiles.compuscene.net/elasticsearch/elasticsearch-prometheus-exporter-${PROMETHEUS_EXPORTER_VERSION}.zip

ENTRYPOINT ["/usr/local/bin/searchguard-entrypoint.sh"]
# Dummy overridable parameter parsed by entrypoint
CMD ["eswrapper"]