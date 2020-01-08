FROM nvidia/cuda:10.0-cudnn7-runtime-ubuntu18.04

RUN apt-get update && \
    apt-get -y install \
    python3-dev \
    python3-pip \
    build-essential \
    wget \
    bzip2 \
    ca-certificates \
    clang \
    git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

WORKDIR /usr/src/app
ONBUILD COPY requirements.txt /
ONBUILD RUN pip3 install -r /requirements.txt

ONBUILD COPY . /usr/src/app
ONBUILD RUN pip3 install .

