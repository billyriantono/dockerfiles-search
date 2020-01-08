ARG DOCKER_REGISTRY=docker.io
ARG FROM_IMG_REPO=qnib
ARG FROM_IMG_NAME="uplain-init"
ARG FROM_IMG_TAG="bionic-2018-12-23.1"
ARG FROM_IMG_HASH=""
FROM ${DOCKER_REGISTRY}/${FROM_IMG_REPO}/${FROM_IMG_NAME}:${FROM_IMG_TAG}${DOCKER_IMG_HASH}

ENV DEBIAN_FRONTEND=noninteractive \
    DEBCONF_NONINTERACTIVE_SEEN=true

ENV REPO_VER=1704_9.0.176-1
ENV CUDA_MAJOR_VER=9
ENV CUDA_MINOR_VER=0
ENV CUDA_PATCH_VER=176-1
ENV CUDA_DRV_MAJOR_VER=390
ENV CUDA_DRV_MINOR_VER=30
ENV CUDA_DRV_PATCH_VER=0ubuntu1
ARG UBUNTU_VER=1704

LABEL platform.features=nvidia-${CUDA_DRV_MAJOR_VER}-${CUDA_DRV_MINOR_VER}

RUN apt-get update \
 && apt-get install -y --no-install-recommends wget gnupg2 \
 && rm -rf /var/lib/apt/lists/*
RUN wget --no-check-certificate -c -v -nc https://developer.download.nvidia.com/compute/cuda/repos/ubuntu${UBUNTU_VER}/x86_64/cuda-repo-ubuntu${REPO_VER}_amd64.deb \
 && dpkg -i cuda-repo-ubuntu${REPO_VER}_amd64.deb \
 && apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu${UBUNTU_VER}/x86_64/7fa2af80.pub
RUN apt-get update \
 && apt-get install -y -o Dpkg::Options::="--force-overwrite" --no-install-recommends \
       nvidia-${CUDA_DRV_MAJOR_VER}=${CUDA_DRV_MAJOR_VER}.${CUDA_DRV_MINOR_VER}-${CUDA_DRV_PATCH_VER} \
       cuda-${CUDA_MAJOR_VER}-${CUDA_MINOR_VER}=${CUDA_MAJOR_VER}.${CUDA_MINOR_VER}.${CUDA_PATCH_VER} \
 && rm -rf /var/lib/apt/lists/*
LABEL org.qnib.nvidia.cuda.drv.version=${CUDA_DRV_MAJOR_VER}.${CUDA_DRV_MINOR_VER}
