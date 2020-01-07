ARG UBUNTU_VERSION=16.04

ARG CUDA=10.0
FROM nvidia/cuda:${CUDA}-base-ubuntu${UBUNTU_VERSION} as base
ARG CUDA=10.0
ARG CUDADASH=10-0
ARG CUDNN=7.6.5.32-1
ARG PYTHON3=python3.7
ARG TF_PACKAGE=tensorflow-gpu==2.0.0

RUN apt-get update \
        && apt-get install nvinfer-runtime-trt-repo-ubuntu1604-5.0.2-ga-cuda${CUDA} \
        && apt-get update \
        && apt-get install -y --no-install-recommends \
            cuda-command-line-tools-${CUDADASH} \
            cuda-cublas-${CUDADASH} \
            cuda-cufft-${CUDADASH} \
            cuda-curand-${CUDADASH} \
            cuda-cusolver-${CUDADASH} \
            cuda-cusparse-${CUDADASH} \
            libnvinfer5=5.0.2-1+cuda${CUDA} \
            libcudnn7=${CUDNN}+cuda${CUDA} \
            libfreetype6-dev \
            libhdf5-serial-dev \
            libzmq3-dev \
            pkg-config \
            build-essential \
            software-properties-common \
            curl \
            unzip \
            wget \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

ENV LD_LIBRARY_PATH /usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH
ENV LANG C.UTF-8

RUN add-apt-repository ppa:deadsnakes/ppa \
        && apt-get update \
        && apt-get install -y \
            ${PYTHON3} \
            ${PYTHON3}-dev \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

RUN wget https://bootstrap.pypa.io/get-pip.py \
      && ${PYTHON3} get-pip.py

RUN ${PYTHON3} -m pip --no-cache-dir install --upgrade \
    pip \
    setuptools

RUN ${PYTHON3} -m pip install --upgrade ${TF_PACKAGE}
