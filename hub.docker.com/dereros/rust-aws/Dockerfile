FROM ubuntu:18.04

RUN apt update && \
    apt install -y curl python-pip && \
    pip install awscli && \
    curl https://sh.rustup.rs -sSf | sh -s -- -y

ENV PATH=/root/.cargo/bin
