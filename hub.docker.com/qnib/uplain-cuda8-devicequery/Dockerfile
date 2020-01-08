ARG FROM_IMG_REGISTRY=docker.io
ARG FROM_IMG_REPO=qnib
ARG FROM_IMG_NAME="uplain-cuda8"
ARG FROM_IMG_TAG="latest"
ARG FROM_IMG_HASH=""
FROM ${FROM_IMG_REGISTRY}/${FROM_IMG_REPO}/${FROM_IMG_NAME}:${FROM_IMG_TAG}${DOCKER_IMG_HASH}

RUN cd /usr/local/cuda-8.0/samples/1_Utilities/deviceQuery \
 && make EXTRA_NVCCFLAGS=--cudart=shared
CMD ["/usr/local/cuda-8.0/samples/1_Utilities/deviceQuery/deviceQuery"]
