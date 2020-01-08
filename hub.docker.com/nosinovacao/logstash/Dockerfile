FROM docker.elastic.co/logstash/logstash-oss:6.2.4

LABEL maintainer="NOS Inovação SA"

ARG ADLS_VERSION=1.2.0
ENV ADLS_VERSION $ADLS_VERSION

ARG LOGSTASH_FILTER_CIPHER_VERSION=3.0.1
ENV LOGSTASH_FILTER_CIPHER_VERSION $LOGSTASH_FILTER_CIPHER_VERSION

RUN bin/logstash-plugin install --version $ADLS_VERSION logstash-output-adls
RUN bin/logstash-plugin install --version $LOGSTASH_FILTER_CIPHER_VERSION logstash-filter-cipher