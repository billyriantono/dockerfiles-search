FROM elixir:1.9.0-alpine
RUN apk add --update git build-base nodejs npm yarn python
RUN mix local.hex --force && \
  mix local.rebar --force
