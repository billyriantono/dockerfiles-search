FROM ubuntu:latest

ENV TARGET=x86_64-unknown-linux-musl

RUN apt-get update && \
    apt-get install \
        curl \
        gcc \
        musl-tools \
        -y

RUN curl https://sh.rustup.rs -sSf -o /tmp/rustup-init.sh; \
    sh /tmp/rustup-init.sh -y --default-toolchain nightly; \
    ~/.cargo/bin/rustup target add --toolchain nightly ${TARGET}; \
    ~/.cargo/bin/rustup component add rustfmt;

