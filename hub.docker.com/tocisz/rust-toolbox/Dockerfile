FROM ubuntu

RUN apt-get update && \
    apt-get install -y gcc curl && \
    rm -rf /var/lib/apt/lists/*

ENV RUSTUP_HOME=/rust
ENV CARGO_HOME=/rust

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y
VOLUME /root
WORKDIR /root

RUN echo "source /rust/env" >> /etc/bash.bashrc
