# Keras, TensorFlow, Python2, cuda and cuDNN (GPU) 
# and some extra packages (opencv, scipy, sklearn, etc)

FROM nvidia/cuda:10.0-cudnn7-runtime-ubuntu16.04

USER root

# install packages
RUN apt-get update -qq \
 && apt-get install --no-install-recommends -y \
    # install essentials
    build-essential \
    git \
    # install python 2
    python \
    python-dev \
    python-pip \
    python-setuptools \
    python-wheel \
    pkg-config \
    # requirements for numpy
    libopenblas-base \
    python-numpy \
    python-scipy \
    # requirements for keras
    python-h5py \
    python-yaml \
    python-pydot \
    # extra packages
    vim \
    python-sklearn \
    python-tk \
    ffmpeg \
    frei0r-plugins \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# update pip
RUN pip install --upgrade pip

# manually update numpy
RUN pip --no-cache-dir install -U numpy==1.14.5

ARG TENSORFLOW_VERSION=1.14.0
ARG TENSORFLOW_DEVICE=gpu
ARG TENSORFLOW_APPEND=_gpu
RUN pip --no-cache-dir install https://storage.googleapis.com/tensorflow/linux/${TENSORFLOW_DEVICE}/tensorflow${TENSORFLOW_APPEND}-${TENSORFLOW_VERSION}-cp27-none-linux_x86_64.whl

ARG KERAS_VERSION=2.3.1
ENV KERAS_BACKEND=tensorflow
RUN pip --no-cache-dir install --no-dependencies git+https://github.com/fchollet/keras.git@${KERAS_VERSION}

# install opencv
RUN pip install opencv-python

# debug
RUN pip install pudb

# matplotlib
RUN pip install matplotlib

WORKDIR /app/
