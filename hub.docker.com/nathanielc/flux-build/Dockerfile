# This file describes an image that is capable of building Flux.

FROM golang:1.12

# Install common packages
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    libtinfo5 \
    ruby \
    ca-certificates curl file \
    build-essential cmake \
    autoconf automake autotools-dev libtool xutils-dev && \
    rm -rf /var/lib/apt/lists/*

# Install ragel
ENV RAGEL_VERSION=6.10
RUN curl http://www.colm.net/files/ragel/ragel-${RAGEL_VERSION}.tar.gz -O && \
    tar -xzf ragel-${RAGEL_VERSION}.tar.gz && \
    cd ragel-${RAGEL_VERSION}/ && \
    ./configure --prefix=/usr/local && \
    make && \
    make install && \
    cd .. && rm -rf ragel-${RAGEL_VERSION}*
ENV PATH="/usr/local/bin:${PATH}"

ENV FLATBUFFERS_VERSION=1.11.0
RUN curl -LS https://github.com/google/flatbuffers/archive/v${FLATBUFFERS_VERSION}.tar.gz | gunzip -c | tar x && \
    mkdir flatbuffers-${FLATBUFFERS_VERSION}/build && \
    cd flatbuffers-${FLATBUFFERS_VERSION}/build && \
    cmake -G "Unix Makefiles" .. && \
    make && make install && \
    cd ../.. && rm -rf flatbuffers-${FLATBUFFERS_VERSION}

# Install and configure openssl - needed for proper Rust install
ENV SSL_VERSION=1.0.2t

RUN curl https://www.openssl.org/source/openssl-$SSL_VERSION.tar.gz -O && \
    tar -xzf openssl-$SSL_VERSION.tar.gz && \
    cd openssl-$SSL_VERSION && ./config && make depend && make install && \
    cd .. && rm -rf openssl-$SSL_VERSION*

ENV OPENSSL_LIB_DIR=/usr/local/ssl/lib \
    OPENSSL_INCLUDE_DIR=/usr/local/ssl/include \
    OPENSSL_STATIC=1

# Install Clang
RUN curl -SL http://releases.llvm.org/8.0.0/clang+llvm-8.0.0-x86_64-linux-gnu-ubuntu-18.04.tar.xz \
    | tar -xJC . && \
    mv clang+llvm-8.0.0-x86_64-linux-gnu-ubuntu-18.04 clang_8.0.0

ENV PATH="/go/clang_8.0.0/bin:${PATH}" \
    LD_LIBRARY_PATH="/clang_8.0.0/lib:${LD_LIBRARY_PATH}" \
    CC=clang


# Add builder user
ENV UNAME=builder
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID -o $UNAME
RUN useradd -m -u $UID -g $UNAME -s /bin/bash $UNAME
USER $UNAME
ENV HOME=/home/$UNAME

# Install Rust
RUN curl https://sh.rustup.rs -sSf | \
    sh -s -- --default-toolchain stable -y
ENV PATH="$HOME/.cargo/bin:${PATH}"
RUN rustup component add rustfmt

# Install wasm-pack and sccache
RUN cargo install wasm-pack sccache
RUN rustup component add rust-std --target wasm32-unknown-unknown

# Use sccache rustc wrapper for friendly build caching
ENV RUSTC_WRAPPER=sccache

WORKDIR $HOME

