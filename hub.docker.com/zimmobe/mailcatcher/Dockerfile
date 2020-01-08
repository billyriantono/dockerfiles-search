FROM alpine:3.4

ENV MAILCATCHER_VERSION=0.6.4

RUN apk add --no-cache \
        ruby ruby-bundler ruby-irb ruby-json ruby-rake ruby-bigdecimal ruby-io-console \
        libstdc++ sqlite-libs openssl

RUN apk add --no-cache --virtual .build-deps build-base ruby-dev sqlite-dev \
    && gem install --no-document mailcatcher -v ${MAILCATCHER_VERSION} \
    && apk del .build-deps

EXPOSE 1025 1080

CMD ["mailcatcher", "-f", "--ip=0.0.0.0"]
