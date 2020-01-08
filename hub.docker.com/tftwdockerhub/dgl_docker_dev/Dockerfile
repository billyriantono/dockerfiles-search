# for a docker image with:
# CUDA 9.0 + cuDNN 7.x
# Anaconda 5.2 (python 3.6)
# PyTorch 1.0
# DGL
# Deep Graph Library

FROM tftwdockerhub/gpu-pytorch:latest

# the maintainer information
LABEL maintainer "TeleWare Data Scientist <teng.fu@teleware.com>"

# pip install dgl
RUN pip --no-cache-dir install dgl

# setup the computation backend
# change the backend by uncomment the specific line
ENV DGLBACKEND pytorch
# ENV DGLBACKEND mxnet
# ENV DGLBACKEND numpy

# setup the working directory
WORKDIR /app