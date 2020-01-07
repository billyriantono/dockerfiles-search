FROM mjcloutier/elixir:alpine-edge
MAINTAINER mjcloutier <viotech@comcast.net>
RUN apk --no-cache add -U nodejs nodejs-npm inotify-tools libsass libsass-dev sassc \
    && mix archive.install https://github.com/phoenixframework/archives/raw/master/phx_new.ez --force
