FROM ruby:2.5-alpine3.7

ENV TRAVIS_CLI_VERSION 1.8.9

# Install build dependencies
RUN apk add --no-cache --virtual .build-deps \
    gcc=6.4.0-r5 \
    libc-dev=0.7.1-r0 \
    make=4.2.1-r0

# Install persistant dependencies
RUN apk add --no-cache --virtual .persistent-deps \
    git=2.15.2-r0

RUN gem install travis --version "${TRAVIS_CLI_VERSION}"

RUN apk del .build-deps

ENTRYPOINT ["travis"]

CMD ["--help"]
