FROM ubuntu:16.04

# Install packages
RUN apt-get update && apt-get -y install curl gcc

# Install Rust
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain nightly-2017-03-24
ENV PATH $PATH:/root/.cargo/bin
