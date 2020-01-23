FROM ruby:alpine
MAINTAINER Andrew Molyuk <andrew.molyuk@gmail.com>

ARG ENVTPL_VERSION=0.2.3
ARG BUILD_DATE
ARG VCS_REF

ENV CLIENT_HOST_DEV=/dev \
    CLIENT_HOST_PROC=/proc \
    CLIENT_HOST_SYS=/sys

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/andrewmolyuk/docker-sensu.git" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.schema-version="1.0.0"

RUN apk update --no-cache && \
    apk add -qU --no-cache \
        bash \
        build-base \
        curl-dev \
        curl \
        libffi-dev \
        ruby-bundler \
        ruby-dev \
        ruby-io-console \
        libxml2-dev \
        libxslt-dev \
        nodejs && \
    \
    curl -Ls https://github.com/arschles/envtpl/releases/download/${ENVTPL_VERSION}/envtpl_linux_amd64 > /usr/local/bin/envtpl && \
    chmod +x /usr/local/bin/envtpl && \
    \
    gem install sensu && \
    \
    gem cleanup && \
    rm -rf \
        /usr/lib/ruby/gems/*/cache/* \
        /var/cache/apk/* \
        /tmp/* \
        /var/tmp/*

VOLUME ["/var/log/sensu", "/etc/sensu/conf.d"]

EXPOSE 4567

COPY bin /bin/
COPY templates /etc/sensu/templates/
ENTRYPOINT ["sh", "/bin/start.sh"]
