ARG DOCKER_REGISTRY=docker.io
ARG FROM_IMG_REPO="library"
ARG FROM_IMG_NAME="ubuntu"
ARG FROM_IMG_TAG="18.04"
ARG FROM_IMG_HASH=""
FROM ${DOCKER_REGISTRY}/${FROM_IMG_REPO}/${FROM_IMG_NAME}:${FROM_IMG_TAG}${DOCKER_IMG_HASH}

RUN apt-get update \
 && apt-get install -y --no-install-recommends pandoc \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
 && apt-get install -y --no-install-recommends texlive-latex-base texlive-fonts-recommended texlive-fonts-extra texlive-latex-extra \
 && rm -rf /var/lib/apt/lists/*
WORKDIR /data

RUN apt-get update \
 && apt-get install -y --no-install-recommends lmodern \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
 && apt-get install -y --no-install-recommends make \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
 && apt-get install -y --no-install-recommends pandoc-citeproc \
 && rm -rf /var/lib/apt/lists/*

