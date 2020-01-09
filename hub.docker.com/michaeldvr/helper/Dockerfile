FROM ubuntu:16.04
LABEL maintainer="Michael Devara <michael.devara@gmail.com>"
LABEL description="Base Ubuntu 16.04"

RUN APT_INSTALL="apt-get install -y --no-install-recommends" && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
    tree \
    wget
