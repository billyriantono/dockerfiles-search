FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

LABEL maintainer 'alexander.morosow@gmail.com'

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        wget \
        software-properties-common \
        python3-pip \
 && add-apt-repository -y ppa:jonathonf/python-3.6 \
 && apt-get update \
 && apt-get install -y python3.6 python3.6-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# pip has to be installed before setuptools, setuptools has to be installed before tensorflow
RUN python3.6 -m pip install --no-cache-dir -U pip
RUN python3.6 -m pip install --no-cache-dir -U setuptools
# also useful
RUN python3.6 -m pip install --no-cache-dir requests numpy scipy pandas quandl imageio
RUN python3.6 -m pip install --no-cache-dir tensorflow-gpu==1.12.0
RUN ln -s /usr/bin/python3.6 /usr/bin/python
