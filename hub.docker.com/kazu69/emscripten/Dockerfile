FROM kazu69/node:8.7.0
MAINTAINER kazu69

RUN echo http://dl-cdn.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories \
     && apk --no-cache add emscripten emscripten-libs-asmjs emscripten-libs-wasm

RUN echo http://dl-cdn.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories \
    && apk --no-cache add binaryen cmake clang \
    &&  rm -rf /var/cache/apk/*

RUN git clone --recursive https://github.com/WebAssembly/wabt \
    && cd wabt \
    && make
