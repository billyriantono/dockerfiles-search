FROM alpine:3.5
MAINTAINER John Endean <john.endean@vualto.com>

ENV BUILD_PACKAGES bash curl-dev build-base rsyslog-hiredis
ENV RUBY_PACKAGES ruby ruby-io-console ruby-dev ruby-bundler ruby-bigdecimal

COPY deployment /deployment

RUN apk upgrade && \
    apk update && \
    apk add $BUILD_PACKAGES && \
    apk add $RUBY_PACKAGES && \
    apk add rsyslog && \
    gem update --system -N && \
    echo "gem: --no-ri --no-rdoc" > ~/.gemrc && \
    chmod 755 /deployment/rsyslog.sh && \
    mv /deployment/rsyslog.conf /etc && \
    mkdir /etc/rsyslog.d && \
    mkdir /var/spool/rsyslog && \
    addgroup syslog && \
    adduser -DG syslog syslog && \
    chown syslog:syslog /var/spool/rsyslog && \
    rm -rf /var/cache/apk/*
