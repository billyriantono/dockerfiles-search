FROM elixir:1.4.5-slim as builder
MAINTAINER Sam Davies <sampdavies@nested.com>

RUN apt-get -qq update
RUN apt-get -qq install git build-essential

RUN mix local.hex --force && \
    mix local.rebar --force && \
    mix hex.info

WORKDIR /app
ENV MIX_ENV prod

COPY mix.exs mix.exs
COPY mix.lock mix.lock

RUN mix deps.get

COPY . .

RUN mix release --env=$MIX_ENV

FROM debian:jessie-slim

# locale ENV settings necessary to avoid warnings by Elixir
ENV LC_ALL=en_US.UTF-8
ENV LANG="en_US.UTF-8"
ENV LC_CTYPE="en_US.UTF-8"

RUN apt-get -qq update
RUN apt-get -qq install libssl1.0.0 libssl-dev
WORKDIR /app
COPY --from=builder /app/_build/prod/rel/eggl .

ENV MIX_ENV prod
ENV PORT=80
EXPOSE $PORT
CMD ["./bin/eggl", "foreground"]
