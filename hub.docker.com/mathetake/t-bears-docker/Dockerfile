FROM ubuntu:18.04

# Install required packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3.6-dev \
    python3-pip \
    python3-setuptools \
    gcc \
    git \
    pkg-config \
    libsecp256k1-dev \
    rabbitmq-server \
    locales \
    vim-tiny \
    lsof \
    && locale-gen en_US.UTF-8 \
    && pip3 install wheel

RUN pip3 install -U pip 

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN pip install git+https://github.com/icon-project/t-bears.git@master \
    && apt-get autoremove -y && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /root/.cache/pip
