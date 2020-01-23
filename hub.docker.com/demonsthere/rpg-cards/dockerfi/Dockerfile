FROM rust:latest

RUN rustup default nightly
RUN cargo install diesel_cli --no-default-features --features "postgres"
RUN rustup component add rustfmt-preview --toolchain nightly
