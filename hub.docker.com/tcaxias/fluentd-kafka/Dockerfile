FROM alpine:edge
MAINTAINER Tiago Caxias http://github.com/tcaxias
WORKDIR /app

ENV \
    PKGS="ruby ruby-irb" \
    DEPS="ruby-dev build-base zlib-dev" \
    GEMS="fluentd fluent-plugin-kafka json fluent-plugin-record-modifier \
            fluent-plugin-parser fluent-plugin-rewrite-tag-filter"

RUN \
    apk --no-cache --update add $PKGS $DEPS && \
    gem install $GEMS --no-ri --no-rdoc && \
    apk --no-cache del $DEPS

ADD fluent.conf /etc/

CMD ["fluentd", "-qc", "/etc/fluent.conf"]
