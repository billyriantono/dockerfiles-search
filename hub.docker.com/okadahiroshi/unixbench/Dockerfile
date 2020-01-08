FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive LANG=C LC_ALL=C

RUN apt update &&\
    apt install -y make gcc perl git &&\
    git clone --depth 1 https://github.com/kdlucas/byte-unixbench.git &&\
    apt remove -y git &&\
    apt autoremove -y &&\
    apt clean &&\
    rm -rf /var/lib/apt/lists/*

WORKDIR /byte-unixbench/UnixBench


CMD ./Run
