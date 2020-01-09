FROM ubuntu:bionic

ARG llvmver=3.9

RUN apt-get update && apt-get install -y \
    # Install pre-reqs
    ca-certificates \
    build-essential \
    # Install Tools
    clang-$llvmver \
    lldb-$llvmver \
    libc++-dev \
    libc++abi-dev \
    cmake \
 && rm -rf /var/lib/apt/lists/*

RUN ln /usr/bin/clang-$llvmver /usr/bin/clang
RUN ln /usr/bin/clang++-$llvmver /usr/bin/clang++
