FROM node:8-slim

RUN curl https://sh.rustup.rs -sSf | sh -s -- --default-toolchain stable -y
RUN export PATH=$HOME/.cargo/bin:$PATH
RUN apt-get update && apt-get upgrade -y && apt-get install -y kcov
RUN rm -rf /var/lib/apt/lists/*
