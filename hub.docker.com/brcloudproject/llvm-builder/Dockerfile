FROM nvcr.io/nvidia/cuda:9.0-devel-ubuntu16.04
MAINTAINER Hervé Yviquel <hyviquel@gmail.com>

ENV BRCLOUD_LLVM_REPO_PATH /root/llvm-project
ENV UPSTREAM_LLVM_REPO_URL https://github.com/llvm/llvm-project.git

RUN apt-get update; apt-get install -y --no-install-recommends cmake  git build-essential cmake pkg-config python python-psutil libelf-dev libffi-dev ninja-build ca-certificates mpich libmpich-dev; rm -rf /var/lib/apt/lists/*

RUN git clone https://gitlab.com/brcloud/llvm-project.git $BRCLOUD_LLVM_REPO_PATH
WORKDIR $BRCLOUD_LLVM_REPO_PATH
RUN git remote add upstream $UPSTREAM_LLVM_REPO_URL; git fetch upstream
