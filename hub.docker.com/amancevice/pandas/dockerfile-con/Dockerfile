FROM ruby:2.4.0-slim
MAINTAINER Alexandr Polyakov <alvlapo+github@gmail.com>

RUN apt-get update && apt-get install -qq -y \
    build-essential \
    patch \
    nodejs \
    libsqlite3-dev \
    libpq-dev \
    ruby-dev \
    zlib1g-dev \
    liblzma-dev \
    libgmp3-dev \
    --fix-missing --no-install-recommends

RUN apt-get autoremove -yq \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY Gemfile /tmp/Gemfile

RUN gem update --system \
    && gem install --no-document --file /tmp/Gemfile
