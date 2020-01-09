FROM rust:1.38 as AGBuilder

WORKDIR /app
RUN rustup target add x86_64-unknown-linux-musl

COPY . .
RUN cargo build --manifest-path=./runu-agent/Cargo.toml --release --target=x86_64-unknown-linux-musl

FROM ubuntu:18.04

RUN apt-get update -y \
  && apt-get upgrade -y \
  && apt-get install -y build-essential net-tools slirp iproute2 iputils-ping socat dnsutils

COPY libuml/scripts/init.sh /sbin/init.sh
COPY --from=AGBuilder /app/runu-agent/target/x86_64-unknown-linux-musl/release/runu-agent /usr/bin/runu-agent
