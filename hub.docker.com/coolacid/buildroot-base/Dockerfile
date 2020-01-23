FROM debian:buster-slim

ARG VERSION=master
RUN echo "Building version: ${VERSION}"
RUN apt-get update; apt-get install -y --no-install-recommends \
    git \
    build-essential \
    ca-certificates \
    file \
    wget \
    cpio \
    unzip \
    rsync \
    bc \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN useradd -r buildroot
WORKDIR /build
RUN chown buildroot /build
USER buildroot
RUN git clone --branch ${VERSION} --depth 1 git://git.buildroot.net/buildroot
WORKDIR /build/buildroot
