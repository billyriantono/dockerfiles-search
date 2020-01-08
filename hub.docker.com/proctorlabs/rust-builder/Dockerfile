FROM rust:1.38-buster

RUN apt-get update && apt-get install -y \
    musl-dev \
    musl-tools && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    rustup target add x86_64-unknown-linux-musl && \
    cargo install cargo-make cargo-deb cargo-readme && \
    rm -rf /usr/local/cargo/registry
