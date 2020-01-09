FROM debian:stretch
LABEL maintainer="st3ph4n"

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
    gcc-arm-none-eabi \
    cmake

RUN mkdir /build
WORKDIR /build
