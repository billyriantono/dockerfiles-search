FROM nvidia/cuda:9.0-devel-ubuntu16.04

ENV CUDNN_VERSION=7.0.5.15-1+cuda9.0
ENV TENSORFLOW_VERSION=1.10.0
ENV KERAS_VERSION=2.2.0
ENV PYTHON_VERSION=3.5

RUN echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list
RUN apt-get update && apt-get install -y \
        libcudnn7=$CUDNN_VERSION \
        python-opencv \
        python$PYTHON_VERSION \
        python$PYTHON_VERSION-dev

RUN apt-get install -y cmake wget curl git vim
RUN ln -sf /usr/bin/python$PYTHON_VERSION /usr/bin/python

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
    rm get-pip.py

RUN pip install --no-cache-dir tensorflow-gpu==$TENSORFLOW_VERSION keras==$KERAS_VERSION 
RUN pip install --no-cache-dir h5py opencv_python pandas matplotlib


