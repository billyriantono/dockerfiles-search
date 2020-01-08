FROM ruby:2.6.3-alpine3.10

RUN apk add --update --no-cache \
  build-base \
  libsodium-dev \
  nodejs \
  unzip \
  sqlite-dev \
  git \
  # for nokogiri
  ruby-dev \
  libxml2-dev \
  libxslt-dev \
  pcre-dev \
  libffi-dev \
  zlib \
  zlib-dev \
  openssl \
  openssl-dev \
  yarn

RUN node -v
RUN ruby -v
RUN git --version
# RUN openssl -v

CMD [ "irb" ]