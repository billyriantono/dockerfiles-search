ARG FROM_IMG_REGISTRY=docker.io
ARG FROM_IMG_REPO=qnib
ARG FROM_IMG_NAME="uplain-cuda8"
ARG FROM_IMG_TAG="8.0.61-1.3"
ARG FROM_IMG_HASH=""
FROM ${FROM_IMG_REGISTRY}/${FROM_IMG_REPO}/${FROM_IMG_NAME}:${FROM_IMG_TAG}${DOCKER_IMG_HASH}

ARG NV_URL=http://developer.download.nvidia.com/compute/redist/cudnn
# NV_CUDA_VER is set by parent
ENV NV_CUDNN_VER=6.0
RUN echo ">> Downloading ${NV_URL}/v${NV_CUDNN_VER}/cudnn-${NV_CUDA_VER}-linux-x64-v${NV_CUDNN_VER}.tgz" \
 && wget -qO - ${NV_URL}/v${NV_CUDNN_VER}/cudnn-${NV_CUDA_VER}-linux-x64-v${NV_CUDNN_VER}.tgz | tar xfz - -C /usr/local/cuda/ --strip-components=1
