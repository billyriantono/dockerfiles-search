FROM elixir:1.9.1-alpine
LABEL maintainer="Stefan Mojsilovic <stefan.mojsilovic90@gmail.com>"
LABEL description="Alpine Linux base image with Elixir, Erlang, Hex, gcc, g++ used to run code in the container for development purposes"

ENV TERM=xterm

RUN \
  apk update && \
  apk add git make g++ wget curl inotify-tools && \
  rm -rf /var/cache/apk/*
RUN \
  mix local.hex --force && \
  mix local.rebar --force
