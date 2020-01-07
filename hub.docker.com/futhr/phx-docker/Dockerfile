FROM resuelve/elixir:latest

MAINTAINER Tobias Bohwalli <hi@futhr.io>

RUN apk --no-cache add -U nodejs nodejs-npm yarn inotify-tools libsass libsass-dev sassc
RUN mix archive.install --force https://github.com/phoenixframework/archives/raw/master/phx_new.ez
RUN mix local.rebar --force
RUN mix local.hex --force

ENV QT_QPA_PLATFORM=offscreen

RUN apk add --update-cache xvfb dbus ttf-freefont fontconfig
RUN rm -rf /var/cache/apk/*

# Show installed versions
RUN mix hex.info && node -v && npm -v && yarn -v

# VOLUME /app/src/deps
# VOLUME /app/src/_build

WORKDIR /code
