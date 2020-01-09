ARG ALPINE_VERSION=3.10
ARG RUBY_VERSION=2.6.3
FROM ruby:$RUBY_VERSION-alpine$ALPINE_VERSION

ARG SOLARGRAPH_VERSION=0.35.2

RUN apk --update add --no-cache --virtual .builddeps \
  gcc \
  make \
  musl-dev \
  && gem install --no-document solargraph --version $SOLARGRAPH_VERSION \
  && apk del .builddeps
RUN install -m 600 -d /data
WORKDIR /data
ENTRYPOINT ["/usr/local/bundle/bin/solargraph"]
CMD ["--help"]
