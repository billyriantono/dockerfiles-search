FROM ubuntu:18.04

MAINTAINER xenodata lab., Inc. <development@xenodata-lab.com>

ENV RUST_VERSION=1.29.1

RUN apt-get update
RUN apt-get install -y \
      build-essential \
      ca-certificates \
      curl \
      git \
      libssl-dev \
      pkg-config

RUN curl -sO https://static.rust-lang.org/rustup/dist/x86_64-unknown-linux-gnu/rustup-init && \
      chmod +x rustup-init
RUN ./rustup-init -y --default-toolchain $RUST_VERSION --no-modify-path && \
      rm -rf rustup-init

ENV PATH $PATH:/root/.cargo/bin

CMD ["/bin/bash"]
