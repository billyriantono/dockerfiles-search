FROM alpine:latest

# Elixir requires UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8


RUN apk update

RUN apk add curl wget git make
RUN apk add openssl
RUN apk add erlang erlang-crypto
RUN apk add elixir

ENV PHOENIX_VERSION 1.1.4


RUN wget "https://github.com/phoenixframework/archives/raw/master/phoenix_new-$PHOENIX_VERSION.ez" -O /tmp/$PHOENIX_VERSION.ez

RUN mix archive.install /tmp/$PHOENIX_VERSION.ez
RUN mix local.hex

RUN apk add nodejs

RUN mkdir -p /code

WORKDIR /code
