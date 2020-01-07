FROM berkus/docker-android-ci:latest

# Install rust (experimental)
# Cargo path is already set in the base image (@fixme?)
RUN apt-get update && \
    apt-get install -y --no-install-recommends pkg-config && \
    rm -rf /var/lib/apt/lists/* && \
    mkdir -p /dist && \
    wget -O /dist/rustup-init https://static.rust-lang.org/rustup/dist/x86_64-unknown-linux-gnu/rustup-init && \
    chmod +x /dist/rustup-init && \
    /dist/rustup-init -y --default-toolchain nightly && \
    rm -rf /dist && \
    ~/.cargo/bin/rustup self update && \
    ~/.cargo/bin/rustup update && \
    ~/.cargo/bin/rustup toolchain add stable && \
    ~/.cargo/bin/rustup target add armv7-linux-androideabi aarch64-linux-android wasm32-unknown-unknown && \
    ~/.cargo/bin/rustup component add clippy llvm-tools-preview rls rust-analysis rustfmt

#    ~/.cargo/bin/cargo install cargo-edit cargo-watch cargo-bloat cargo-asm cargo-expand cargo-graph cargo-vendor cargo-release && \
#    ~/.cargo/bin/cargo install --git https://github.com/matthiaskrgr/cargo-cache && \
#    ~/.cargo/bin/cargo cache -i && \
#    ~/.cargo/bin/cargo cache -e && \
#    ~/.cargo/bin/cargo cache -i

# RUN ~/.cargo/bin/cargo install cargo-web -- 0.6.17 fails to detect openssl version
