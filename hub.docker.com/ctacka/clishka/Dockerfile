FROM alpine:latest

RUN apk --no-cache update && apk --no-cache upgrade && apk --no-cache --update add \
    ruby ruby-rake ruby-dev ruby-io-console ruby-bigdecimal ruby-json ruby-bundler \
    libstdc++ g++ make libgpg-error tzdata bash ca-certificates \
    python py-pip py-setuptools ca-certificates curl groff less \
    && echo 'gem: --no-document' > /etc/gemrc \
    && gem install stack_master \
    && pip --no-cache-dir install awsebcli awscli \
    && rm -rf /var/cache/apk/*
