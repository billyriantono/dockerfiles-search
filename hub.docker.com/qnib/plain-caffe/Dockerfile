ARG DOCKER_REGISTRY="docker.io"
ARG FROM_IMG_REPO="qnib"
ARG FROM_IMG_NAME="uplain-init"
ARG FROM_IMG_TAG="18.04"
ARG FROM_IMG_HASH=""
FROM ${DOCKER_REGISTRY}/${FROM_IMG_REPO}/${FROM_IMG_NAME}:${FROM_IMG_TAG}${DOCKER_IMG_HASH}

RUN apt-get -qq update \
 && apt-get install -y caffe-cuda
