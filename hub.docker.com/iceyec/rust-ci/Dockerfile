FROM rust:latest

RUN apt-get -qq update
RUN apt-get install -yqq libcurl4-gnutls-dev libelf-dev libdw-dev \
    binutils-dev libssh2-1-dev libgit2-dev cmake unzip

RUN rustup install nightly beta stable
RUN cargo install cargo-travis
RUN cargo coverage || true