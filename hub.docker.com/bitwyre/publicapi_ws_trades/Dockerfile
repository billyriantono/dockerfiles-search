# Stage 1 - Builder
ARG app_name="publicapi_ws_trades"

FROM rust:1.38.0-slim-buster as builder
ARG app_name
ENV APP_NAME=$app_name
ENV USER=root
WORKDIR /usr/src
RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential cmake autoconf clang pkg-config libssl-dev && \
    cargo new $APP_NAME
WORKDIR /usr/src/$APP_NAME
COPY Cargo.toml .
COPY src ./src
RUN cargo --version && \
    cargo build --release

# Stage 2 - Production Image
FROM ubuntu:18.04
ARG app_name
ENV APP_NAME=$app_name
LABEL maintainer "Yefta Sutanto <yefta@bitwyre.com>, Aditya Kresna <kresna@bitwyre.com>"
RUN useradd -U bitwyre
WORKDIR /home/bitwyre/bin/
COPY --from=builder /usr/src/$APP_NAME/target/release/$APP_NAME .
RUN chown bitwyre:bitwyre $APP_NAME
USER bitwyre
# Define Entry Point
CMD ./$APP_NAME
