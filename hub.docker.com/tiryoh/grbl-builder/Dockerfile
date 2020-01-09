FROM ubuntu:bionic
MAINTAINER tiryoh<tiryoh@gmail.com>

RUN apt-get update -q && \
    apt-get upgrade -yq && \
    apt-get install -yq make gcc-avr avr-libc && \
    rm -rf /var/lib/apt/lists/*
WORKDIR /source
CMD ["make"]
