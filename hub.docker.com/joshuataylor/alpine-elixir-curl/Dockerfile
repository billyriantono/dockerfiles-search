FROM bitwalker/alpine-elixir:1.6.6

MAINTAINER Josh Taylor <joshuataylorx@gmail.com>

RUN apk --update upgrade && apk add --no-cache build-base curl postgresql-client && \
    mix local.rebar --force && \
    mix local.hex --force
