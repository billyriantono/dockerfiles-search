FROM ubuntu:16.04
MAINTAINER Hannes de Jager <hannes.de.jager@gmail.com>

RUN apt-get update \
    && apt-get install -y curl file sudo build-essential
    
RUN curl https://sh.rustup.rs > sh.rustup.rs \
    && sh sh.rustup.rs -y \
    && . $HOME/.cargo/env \
    && echo 'source $HOME/.cargo/env' >> $HOME/.bashrc \
    && rustup update \
    && rustup target add x86_64-unknown-linux-musl

VOLUME /project
WORKDIR /project

