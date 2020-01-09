FROM debian:buster-20190708-slim as fulldevenv

WORKDIR /build

COPY Gemfile Gemfile.lock /build/

RUN apt-get update \
  && apt-get install -y \
    git \
    ruby-dev \
    gcc \
    g++ \
    make \
    libc6-dev \
    zlib1g-dev \
  && rm -rf /var/lib/apt/lists/* \
  && gem install -N bundler -v 1.17.3 \
  && bundle install --deployment

FROM node:12.7.0-buster-slim

COPY --from=fulldevenv /build /rubytooling/

RUN apt-get update \
  && apt-get install --no-install-recommends -y \
    jq \
    python3 \
    python3-pip \
    python3-setuptools \
    python3-wheel \
    ruby \
  && rm -rf /var/lib/apt/lists/* \
  && gem install -N bundler -v 1.17.3 \
  && bundle config gemfile '/rubytooling/Gemfile' \
  && pip3 install 'awscli~=1.16.209'

