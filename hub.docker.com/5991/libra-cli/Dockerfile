FROM debian:9 as builder

# Install dependencies
RUN apt-get update -qq \
    && apt-get install -y --no-install-recommends -qq \
        ca-certificates curl wget sudo git unzip make \
        gcc gcc-multilib g++

# Install Libra dependencies

# -- Rust
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain stable
ENV PATH "$PATH:/root/.cargo/bin"

# -- CMake & Golang
RUN apt-get -y --no-install-recommends -qq install cmake golang

# -- Protobuf
RUN curl -OL https://github.com/protocolbuffers/protobuf/releases/download/v3.8.0/protoc-3.8.0-linux-x86_64.zip \
    && unzip protoc-3.8.0-linux-x86_64.zip -d protoc3 \
    && mv protoc3/bin/* /usr/local/bin/ \
    && mv protoc3/include/* /usr/local/include/

FROM builder

# Clone Libra
RUN git clone https://github.com/libra/libra.git

WORKDIR /libra

# Build CLI
RUN cargo build -p client

ENTRYPOINT ["tail", "-f", "/dev/null"]
