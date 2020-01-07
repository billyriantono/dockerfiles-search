FROM debian:stable-slim

WORKDIR /code
ENV HOME /code
ENV PATH="${HOME}:${HOME}/.cargo/bin:${HOME}/cargo-watch/target/debug:${PATH}"

RUN apt-get update \
    && apt-get install -y curl build-essential git \
    && curl https://sh.rustup.rs -sSf | sh -s -- -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rustup self update \
    && rustup install nightly \
    && rustup default nightly \
    && git clone https://github.com/passcod/cargo-watch.git \
    && cd cargo-watch \
    && cargo build

EXPOSE 8000