FROM ubuntu:16.04

MAINTAINER Pradeep Kumar A.V. <pradeepkumar1025@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV LANG en_US.UTF-8

# System dependencies
RUN apt-get update && apt-get install -y \
    vim \
    git \
    curl \
    wget \
    nano \
    cmake \
    unzip \
    pkg-config \
    imagemagick \
    build-essential > /dev/null

# Miniconda3
ENV PATH /opt/conda/bin:$PATH
ENV LB_LIBRARY_PATH /opt/conda/lib:$LB_LIBRARY_PATH
RUN curl -Ls https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -o /tmp/install-miniconda.sh && \
    /bin/bash /tmp/install-miniconda.sh -b -p /opt/conda && \
    conda update --all -y

# Some Tools
RUN pip install flask click pyyaml

# Jupyter
RUN pip install -q jupyter jupyterlab && \
    jupyter --version
