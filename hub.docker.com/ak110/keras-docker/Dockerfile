FROM nvidia/cuda:10.0-cudnn7-devel

ARG DEBIAN_FRONTEND=noninteractive
ENV PATH=/usr/src/conda/bin:$PATH

RUN set -x && \
    apt-get update && \
    apt-get install --yes --no-install-recommends --allow-downgrades \
        ca-certificates \
        libglib2.0-0 \
        libopencv-core-dev \
        libsm6 \
        libxext6 \
        libxrender1 \
        wget \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN set -x && \
    wget -q https://repo.continuum.io/miniconda/Miniconda3-4.6.14-Linux-x86_64.sh -O conda.sh && \
    echo "718259965f234088d785cad1fbd7de03 *conda.sh" | md5sum -c - && \
    /bin/bash conda.sh -f -b -p /usr/src/conda && \
    conda clean --all --yes && \
    rm conda.sh

COPY requirements.txt ./
ARG PIP_PROXY=$http_proxy
ARG PIP_TRUSTED_HOST=""
ARG PIP_INDEX_URL=""
RUN http_proxy=$PIP_PROXY pip install --no-cache-dir -r requirements.txt

RUN mkdir /usr/src/app
WORKDIR /usr/src/app

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    MPLBACKEND='Agg'
