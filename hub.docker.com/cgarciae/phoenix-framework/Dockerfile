FROM elixir:1.2.5

MAINTAINER Shane Sveller <shane@shanesveller.com>

RUN apt-get update -q && \
    apt-get -y install \
    apt-transport-https \
    curl \
    libpq-dev \
    postgresql-client \
    && apt-get clean -y && \
    rm -rf /var/cache/apt/*

RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
    echo 'deb https://deb.nodesource.com/node_4.x jessie main' > /etc/apt/sources.list.d/nodesource.list && \
    apt-get update -q && \
    apt-get install -y \
    nodejs \
    && apt-get clean -y && \
    rm -rf /var/cache/apt/*

RUN npm install -g npm@3.8.9
RUN mix local.hex --force && \
    mix local.rebar --force

ENV PHOENIX_VERSION 1.1.4

RUN mix archive.install --force https://github.com/phoenixframework/archives/raw/master/phoenix_new-$PHOENIX_VERSION.ez
