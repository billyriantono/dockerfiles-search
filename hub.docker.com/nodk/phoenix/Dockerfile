ARG ELIXIR_VER=latest
FROM elixir:${ELIXIR_VER}

ARG PHOENIX_VER=latest
RUN mix local.hex --force && \
    mix archive.install hex phx_new ${PHOENIX_VER} --force && \
    mix local.rebar --force
