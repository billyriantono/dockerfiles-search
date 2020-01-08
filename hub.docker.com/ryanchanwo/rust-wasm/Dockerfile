FROM rustlang/rust:nightly
LABEL maintainer="ryanchanwo@gmail.com"

# Squash dpkg-preconfigure messages.
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -qqy \
    && apt-get install -qqy --no-install-recommends \
        ca-certificates \
        curl \
        gcc \
        libc6-dev \
        libssl-dev \
    && rustup target add wasm32-unknown-unknown \
    && cargo install -q wasm-bindgen-cli
