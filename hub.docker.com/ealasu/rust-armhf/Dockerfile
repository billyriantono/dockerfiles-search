FROM debian:stretch
WORKDIR /root

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    build-essential ca-certificates curl file xutils-dev libssl-dev pkg-config && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean

RUN curl https://sh.rustup.rs -sSf | \
    sh -s -- --default-toolchain stable -y

ENV PATH=/root/.cargo/bin:$PATH

RUN rustup target add armv7-unknown-linux-gnueabihf

RUN apt-get update && \
    apt-get install -y gcc-arm-linux-gnueabihf && \
    apt-get clean

#RUN apt-get update && \
#    apt-get install --no-install-recommends -y \
#    gdb && \
#    rm -rf /var/lib/apt/lists/* && \
#    apt-get clean
