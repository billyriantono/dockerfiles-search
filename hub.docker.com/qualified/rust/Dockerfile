FROM rust:1.36.0-slim-stretch

RUN set -ex; \
    useradd --create-home codewarrior; \
    mkdir /workspace; \
    chown codewarrior:codewarrior /workspace;

COPY --chown=codewarrior:codewarrior rootfs/workspace/rust /workspace/rust

WORKDIR /workspace

USER codewarrior
ENV USER=codewarrior \
    HOME=/home/codewarrior \
# Allow dead_code to avoid tests from printing warnings about private identifiers
    RUSTFLAGS='-Adead_code'

# download and compile crates
RUN set -ex; \
    cd /workspace/rust; \
    cargo build --tests; \
    rm -rf \
      src/lib.rs \
      target/debug/qualified_rust* \
      target/debug/incremental/qualified_rust* \
    ;
