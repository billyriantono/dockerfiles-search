FROM frolvlad/alpine-glibc:alpine-3.9_glibc-2.29
RUN apk --no-cache add curl bash build-base coreutils findutils patchutils grep procps openssl-dev
ENV RUST_HOME /usr/local/rust
ENV CARGO_HOME /usr/local/cargo
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | bash -s -- \
    --default-host x86_64-unknown-linux-gnu \
    --default-toolchain nightly \
    --no-modify-path \
    -y
ENV PATH $CARGO_HOME/bin:$PATH
