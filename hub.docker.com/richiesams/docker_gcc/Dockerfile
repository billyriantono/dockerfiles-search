FROM ubuntu:bionic

RUN apt-get update \
    # Install pre-reqs
    && apt-get install -y \
        ca-certificates \
        build-essential \
    # Install Tools
        gcc-7 \
        g++-7 \
        cmake \
    && rm -rf /var/lib/apt/lists/*

RUN rm /usr/bin/gcc && ln /usr/bin/gcc-7 /usr/bin/gcc
RUN rm /usr/bin/g++ && ln /usr/bin/g++-7 /usr/bin/g++
