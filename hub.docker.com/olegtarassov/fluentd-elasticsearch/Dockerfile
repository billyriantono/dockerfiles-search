ARG VERSION=v1.8-debian
FROM fluent/fluentd:${VERSION}
ARG ELASTIC_VERSION=3.8.0
LABEL maintainer "Oleg Tarassov <oleg.tarassov@outlook.com>"
LABEL Description="Fluentd docker image with elasticsearch" Elastic_Version="${ELASTIC_VERSION}" Debian_Version="${VERSION}"

USER root
RUN gem install fluent-plugin-elasticsearch --no-document --version ${ELASTIC_VERSION}

USER fluent

