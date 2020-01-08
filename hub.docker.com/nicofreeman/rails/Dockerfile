# 1: Use ruby 2.2.6 as base:
FROM nicofreeman/ruby:2.4.0-alpine

USER root

ENV APP_NAME=rails_api \
    RAILS_VERSION=5.0.1

ARG APP_NAME
ARG RAILS_VERSION

ENV APP_HOME=/usr/src/$APP_NAME \
    PATH=/usr/src/$APP_NAME/bin:$PATH \
    RAILS_VERSION=$RAILS_VERSION

RUN set -ex \
  && runDeps="$( \
    scanelf --needed --nobanner --recursive /usr/local \
      | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
      | sort -u \
      | xargs -r apk info --installed \
      | sort -u \
  )" \
  && apk add --no-cache --virtual .ruby-rundeps $runDeps \
    bzip2 \
    ca-certificates \
    libffi-dev \
    openssl-dev \
    yaml-dev \
    procps \
    zlib-dev \
    build-base \
    tzdata \
    postgresql-dev \
  && gem install bundler --version "$BUNDLER_VERSION" \
  && mkdir -p $APP_HOME \
  && cd $APP_HOME \
  && echo "source 'https://rubygems.org'" > Gemfile \
  && echo "gem 'rails', '~> $RAILS_VERSION'" >> Gemfile  \
  && touch Gemfile.lock \
  && bundle --retry 3 \
  && chown -R $(id $DEV_USER -u) "$GEM_HOME" "$BUNDLE_BIN" "$APP_HOME"

USER $DEV_USER
WORKDIR $APP_HOME
EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0", "-p", "3000"]

COPY gemfile.entrypoint /usr/src/
