FROM nvidia/cuda:8.0-cudnn6-devel-ubuntu16.04
MAINTAINER Yohei Kikuta <diracdiego@gmail.com>

RUN apt-get update && \
    apt-get install -y python3.5 \
    python3-pip \
    python3-dev

RUN pip3 install --upgrade pip

RUN pip3 install tensorflow-gpu \
    jupyter
