#FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

FROM nvidia/cuda:9.0-devel-ubuntu16.04

LABEL maintainer "NVIDIA CORPORATION <cudatools@nvidia.com>"

ENV CUDNN_VERSION 7.0.4.31
LABEL com.nvidia.cudnn.version="${CUDNN_VERSION}"

RUN apt-get update && apt-get install -y wget
RUN wget https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/libcudnn7-dev_7.0.4.31-1+cuda9.0_amd64.deb
RUN wget https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/libcudnn7_7.0.4.31-1+cuda9.0_amd64.deb 

RUN dpkg -i ./libcudnn7_7.0.4.31-1+cuda9.0_amd64.deb && apt-get install -f
RUN dpkg -i ./libcudnn7-dev_7.0.4.31-1+cuda9.0_amd64.deb && apt-get install -f
