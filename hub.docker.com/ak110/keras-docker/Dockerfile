FROM nvidia/cuda:10.1-cudnn7-runtime

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
    wget -q https://repo.continuum.io/miniconda/Miniconda3-4.7.12.1-Linux-x86_64.sh -O conda.sh && \
    echo "81c773ff87af5cfac79ab862942ab6b3 *conda.sh" | md5sum -c - && \
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

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    MPLBACKEND='Agg' \
    TF_FORCE_GPU_ALLOW_GROWTH='true' \
    TF_DETERMINISTIC_OPS='true'
