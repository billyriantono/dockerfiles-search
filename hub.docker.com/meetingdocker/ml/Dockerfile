FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04
#FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
MAINTAINER Heptagram <350526878@qq.com>

# Install basic dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        wget \
        vim \
        openssh-server \
        libfreetype6 \
        libgl1-mesa-dev \
        libglu1-mesa \
        libxi6 \
        libxrender1

# Set locale
ENV LANG C.UTF-8 LC_ALL=C.UTF-8

ENTRYPOINT ["/bin/bash", "-c", "/root/docker-runner-startup"]

# Initialize workspace
RUN mkdir /workspace
WORKDIR /workspace
