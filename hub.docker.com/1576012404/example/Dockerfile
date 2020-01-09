FROM ubuntu:18.04

SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get install -y \
    python3-setuptools \
    python3-pip \
    git \
    libsm6 \
    libxext6 \
    libxrender-dev \
    wget \
    pkg-config

WORKDIR /src
