ARG ELIXIR_VER=1.8.0
ARG ALPINE_VER=3.8

################################
# 1. build 
################################
FROM arcblock/forge_deps:latest as deps

FROM elixir:$ELIXIR_VER-alpine as builder
ARG GTK
RUN apk update && \
  apk upgrade --no-cache && \
  apk add --no-cache \
  wget libbz2 libtool openssl-dev unzip binutils zlib  libstdc++ make cmake git g++ \
  autoconf bzip2-dev automake linux-headers  gmp-dev  python curl nodejs npm openssh sqlite-dev zstd-dev 
WORKDIR /home/arcblock
RUN git config --global url."https://${GTK}:@github.com/".insteadOf "git@github.com:"
COPY .  .
ENV ERLANG_ROCKSDB_OPTS="-DWITH_ZSTD=ON"
#RUN make init
RUN mix local.hex --force && mix local.rebar --force
COPY --from=deps /src /home/arcblock/mix_deps/

RUN MIX_ENV=staging make docker-builds && \
  cd vendors/forge && ERLANG_ROCKSDB_OPTS="-DWITH_ZSTD=ON" mix deps.compile rocksdb && cd ../../ && \ 
  MIX_ENV=staging  make centos 
RUN make copy-release 
RUN mkdir /forge && mkdir /forge/$(cat version) && tar -xf "_build/releases/forge_centos_amd64.tgz" -C /forge/$(cat version)
RUN mkdir /starter && tar -xf "_build/releases/forge_starter_centos_amd64.tgz" -C /starter
RUN mkdir /forge_web && tar -xf "_build/releases/forge_web_centos_amd64.tgz" -C /forge_web
#RUN adduser -S -G arcblock arcblock 
#RUN chown -R arcblock /forge /starter /forge_web
RUN echo "current: $(cat version)" > /forge/release.yml


################################
# 2.Runtime
################################
FROM alpine:$ALPINE_VER
MAINTAINER Paper Huang <shan@arcblock.io>
ENV REPLACE_OS_VARS=true \
  PORT=8211 \
  FORGE_CONFIG=/opt/arcblock/forge_release.toml \
  FORGE_RELEASE=/opt/arcblock/forge/ \
  HOME=/opt/arcblock \
  SHELL=/bin/bash
RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2
RUN apk update && \
  apk upgrade --no-cache && \
  apk add --no-cache \
  bash openssl-dev   bzip2-dev  linux-headers  gmp-dev  zstd-dev 
WORKDIR /opt/arcblock



COPY --from=builder /starter/ ./starter/ 
COPY     --from=builder /forge/ ./forge/  
COPY     --from=builder /forge_web/ ./forge_web 
COPY     --from=builder /home/arcblock/vendors/forge/deps/forge_sdk/priv/forge_release.toml $HOME/forge_release.toml  
RUN chmod -R 777 /opt/arcblock
#RUN  chown arcblock /opt/arcblock && chown -R arcblock /opt/arcblock/
RUN  addgroup -S arcblock && adduser -S -G arcblock arcblock   

USER arcblock     
# forge web
EXPOSE 8210
EXPOSE 28210
EXPOSE 37017
# ipfs
EXPOSE 4369
EXPOSE 28080
EXPOSE 24001
EXPOSE 25001

# tendermint
EXPOSE 28221
EXPOSE 28222
EXPOSE 26656
EXPOSE 26660
ENV FORGE_SOCK_GRPC=tcp://127.0.0.1:28210
#ENTRYPOINT [ "starter/bin/forge_starter foreground" ] 
CMD ["/bin/bash","-c","/opt/arcblock/starter/bin/forge_starter start ;sleep 100; /opt/arcblock/forge_web/bin/forge_web foreground"]

