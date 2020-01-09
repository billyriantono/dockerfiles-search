ARG ELIXIR_VER=1.7.4
ARG ALPINE_VER=3.8
################################
# 1. build 
################################
FROM arcblock/forge_deps as deps

FROM elixir:$ELIXIR_VER-alpine as builder
ARG GTK
RUN apk update && \
  apk upgrade --no-cache && \
  apk add --no-cache \
  wget libbz2 libtool openssl-dev unzip binutils zlib  libstdc++ make cmake git g++ \
  autoconf bzip2-dev automake linux-headers  gmp-dev  python curl nodejs npm openssh
WORKDIR /home/arcblock
RUN git config --global url."https://${GTK}:@github.com/".insteadOf "git@github.com:"
COPY .  .
RUN mix local.hex --force && mix local.rebar --force 
COPY --from=deps /src/_build /home/arcblock/_build
COPY --from=deps /src/deps /home/arcblock/deps
RUN make docker
RUN mkdir /export && tar -xf "_build/releases/forge_docker_amd64.tgz" -C /export




################################
# 2.Runtime
################################
FROM alpine:$ALPINE_VER
EXPOSE 8210
ENV REPLACE_OS_VARS=true \
    PORT=8210 \
    FORGE_CONFIG=forge_release.toml \
    HOME=/home/arcblock \
    SHELL=/bin/bash
WORKDIR /home/arcblock
RUN addgroup -S arcblock && adduser -S -G arcblock arcblock && chown arcblock /home/arcblock && chown -R arcblock /home/arcblock/
RUN apk update && \
  apk upgrade --no-cache && \
  apk add --no-cache \
  bash openssl-dev   bzip2-dev  linux-headers  gmp-dev
USER arcblock
COPY --from=builder /export/ .
COPY --from=builder /home/arcblock/deps/forge_sdk/priv/forge_release.toml $HOME/forge_release.toml 
CMD bin/forge console



    
