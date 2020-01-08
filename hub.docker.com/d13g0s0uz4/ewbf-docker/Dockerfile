#FROM nvidia/cuda:8.0-devel-ubuntu16.04
ARG cuda_tag=8.0-devel-ubuntu16.04
ARG repository=nvidia/cuda
FROM ${repository}:${cuda_tag} as builder

LABEL MAINTAINER "d13g0souz4 <d13g0s0uz4@zoho.com>"

ENV GPU_FORCE_64BIT_PTR 0
ENV GPU_MAX_HEAP_SIZE 100
ENV GPU_USE_SYNC_OBJECTS 1
ENV GPU_MAX_ALLOC_PERCENT 100
ENV GPU_SINGLE_ALLOC_PERCENT 100

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y --no-install-recommends -f install \
    && apt-get install -y --no-install-recommends \
      ca-certificates \
      build-essential \
      curl \
      libleveldb-dev \
      libjsoncpp-dev \
      libjsonrpccpp-dev \
      libboost-all-dev \
      libgmp-dev \
      libreadline-dev \
      libcurl4-gnutls-dev \
      ocl-icd-libopencl1 \
      opencl-headers \
      mesa-common-dev \
      libmicrohttpd-dev \
      tar
RUN update-ca-certificates \
    apt-get clean \
    rm -rf /var/lib/apt/lists/*

RUN curl -sLO https://github.com/d13g0s0uz4/ewbf-docker/files/1627077/Zec.Miner.0.3.4b.Linux.Bin.tar.gz \
   && tar -xzf Zec.Miner.0.3.4b.Linux.Bin.tar.gz \
   && rm -f Zec.Miner.0.3.4b.Linux.Bin.tar.gz

RUN sed -i 's/#error -- unsupported GNU version! gcc versions later than 5 are not supported!/\-\-#error -- unsupported GNU version! gcc versions later than 5 are not supported!/g' \
    /usr/local/cuda/targets/x86_64-linux/include/host_config.h

RUN DEBIAN_FRONTEND=newt
ENTRYPOINT ["./0.3.4b/miner"]
