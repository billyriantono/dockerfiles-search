FROM ubuntu
MAINTAINER vvakame

# setup
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential cmake python2.7 nodejs default-jre git-core \
        curl \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && ln -s /usr/bin/python2.7 /usr/bin/python \
    && ln -s /usr/bin/nodejs /usr/bin/node

# emscripten
# requirements 1.37.0 or higher
RUN cd /root \
    && curl https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz | tar zx \
    && cd ./emsdk_portable \
    && ./emsdk install sdk-incoming-64bit \
    && ./emsdk activate sdk-incoming-64bit \
    && echo "source $HOME/emsdk_portable/emsdk_env.sh" > /root/.bashrc
# wasm2wast & wast2wasm and others
RUN cd /root \
    && git clone --recursive https://github.com/WebAssembly/wabt \
    && cd wabt \
    && make gcc-release
ENV PATH /root/wabt/out/gcc/Release:$PATH

# Rust
ENV PATH /root/.cargo/bin:$PATH
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y \
    && rustup install stable \
    && rustup component add rust-src \
    && rustup target add wasm32-unknown-emscripten \
    && rustup target add asmjs-unknown-emscripten \
    && rustup install nightly \
    && rustup component add rust-src --toolchain nightly \
    && rustup target add asmjs-unknown-emscripten --toolchain nightly \
    && rustup target add wasm32-unknown-emscripten --toolchain nightly \
    && rustup default nightly
