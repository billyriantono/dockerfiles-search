FROM elixir:1.7.2-alpine
MAINTAINER Ronualdo Maciel <raxmac@gmail.com>

RUN apk add --no-cache inotify-tools

ENV PHOENIX_VERSION 1.3.4

RUN mix local.hex --force &&\
    mix local.rebar --force

RUN mix archive.install --force\
  https://github.com/phoenixframework/archives/raw/master/phx_new-$PHOENIX_VERSION.ez

CMD ["bin/ash"]
