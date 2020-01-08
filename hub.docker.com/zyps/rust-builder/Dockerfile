FROM zyps/base-build:latest

ENV RUSTUP_HOME=/usr/local/rustup \
    CARGO_HOME=/usr/local/cargo \
    PATH=/usr/local/cargo/bin:$PATH \
    RUST_VERSION=1.39.0

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --no-modify-path --default-toolchain $RUST_VERSION \
# Init cargo packages index for faster builds
  && . ~/.profile \
  && cargo search serde \
  && apt-get update \
  && apt-get install -y --no-install-recommends capnproto pkg-config libssl-dev libpq-dev \
  && chmod -R a+w $RUSTUP_HOME $CARGO_HOME \
# Clean
  && rm -rf /var/lib/apt/lists/*

ENV PATH "/root/.cargo/bin:${PATH}"
