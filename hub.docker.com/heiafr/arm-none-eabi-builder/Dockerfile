FROM alpine
LABEL maintainer "Jacques Supcik <jacques.supcik@hefr.ch>"

RUN apk add --no-cache -X http://dl-cdn.alpinelinux.org/alpine/edge/testing \
    binutils-arm-none-eabi \
    clang6 \
    clang6-analyzer \
    cmake \
    curl \
    file \
    gcc-arm-none-eabi \
    git \
    llvm6 \
    make \
    newlib-arm-none-eabi \
    python3 \
    unzip

RUN pip3 install --upgrade pip && \
    pip3 install chardet cpplint
