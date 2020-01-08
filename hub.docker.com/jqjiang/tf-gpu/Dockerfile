FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04

VOLUME ["/work"]

RUN apt-get update && apt-get install -y --no-install-recommends python3 python3-pip && \
    pip3 install wheel setuptools && \
    pip3 install tensorflow-gpu==1.14.0 && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /work
