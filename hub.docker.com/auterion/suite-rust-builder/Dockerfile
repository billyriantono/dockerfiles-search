FROM rust:1.40

RUN apt-get update \
  && apt-get install -y cmake unzip libpq5

RUN useradd -m -U rust \
  && mkdir /home/rust/src /home/rust/target /home/rust/cargo \
  && chown -R rust:rust /home/rust/src /home/rust/target /home/rust/cargo

WORKDIR /home/rust/src

ENV CARGO_HOME=/home/rust/cargo
ENV CARGO_TARGET_DIR=/home/rust/target

USER rust

ADD . ./

RUN cargo build --release

