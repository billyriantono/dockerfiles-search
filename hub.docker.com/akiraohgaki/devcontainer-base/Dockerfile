FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update -qq \
    && apt -y --no-install-recommends install apt-utils dialog 2>&1 \
    && apt -y install iproute2 procps lsb-release sudo \
    && apt -y install zsh curl unzip git nano vim build-essential \
    && apt clean \
    && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/tj/n.git -b master --single-branch --depth=1 /tmp/n \
    && (cd /tmp/n && make install) \
    && rm -rf /tmp/n

ENV DEBIAN_FRONTEND=
