FROM rust:1.38.0-slim-stretch

LABEL maintainer="akidsuki <akidsuki@palladion.jp>"

WORKDIR /usr/my_projects
RUN apt-get update -y \
&& apt-get upgrade -y \
&& apt-get install -y libpq-dev clang llvm-dev libclang-dev libssl-dev pkg-config \
&& cargo install diesel_cli --no-default-features --features postgres \
&& cargo install cargo-watch
