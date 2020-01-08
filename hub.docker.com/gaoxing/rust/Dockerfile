FROM ubuntu:18.04

ENV PATH="/root/.cargo/bin:$PATH"

RUN apt-get --yes update \
    && apt-get --yes upgrade \
    && apt-get --yes install \
            vim curl bash git build-essential \
            llvm lldb valgrind binutils-dev \
            libiberty-dev libpopt-dev sudo musl-tools musl-dev \
    && apt-get --yes autoremove \
    && apt-get --yes clean

RUN cd /root \
    && curl -sSf https://sh.rustup.rs | sh -s -- --default-toolchain stable -y

RUN printf '\n\
export PATH=$PATH:/root/.cargo/bin \n\
export USER=root \n\
' >> /root/.bashrc

RUN rustup target add x86_64-unknown-linux-musl

RUN mkdir -p /root/.cargo \
    && printf '[source.crates-io] \n\
    registry = "https://github.com/rust-lang/crates.io-index" \n\
    replace-with = "ustc" \n\
[source.ustc] \n\
    registry = "git://mirrors.ustc.edu.cn/crates.io-index" \n\
    \n\
[build] \n\
    target = "x86_64-unknown-linux-musl" \n\
' > /root/.cargo/config
