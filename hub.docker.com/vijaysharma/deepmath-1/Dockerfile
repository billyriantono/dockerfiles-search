# Start with Theano base image
FROM ubuntu:14.04
MAINTAINER Vijay Sharma <ivnyou.all@gmail.com>

RUN apt-get update && apt-get install -y \
  build-essential \
  gfortran \
  git \
  wget \
  liblapack-dev \
  libopenblas-dev \
  python-dev \
  python-pip \
  python-nose \
  python-numpy \
  python-scipy

# Install bleeding-edge Theano
RUN pip install --upgrade pip
RUN pip install --upgrade six
#RUN pip install --upgrade --no-deps git+git://github.com/Theano/Theano.git
RUN cd /root && git clone git://github.com/Theano/Theano.git
RUN cd /root/Theano && python setup.py develop

# Install optional dependencies
RUN apt-get update && apt-get install -y \
  curl \
  cython \
  python-imaging \
  python-matplotlib \
  python-yaml

# Upgrade six
# RUN pip install --upgrade six
# RUN pip install --upgrade Theano

# Clone Pylearn2 repo and move into it
RUN cd /root && git clone https://github.com/lisa-lab/pylearn2.git && cd pylearn2 && \
  # Install
  python setup.py develop

# Make and set data directory
RUN mkdir /data
ENV PYLEARN2_DATA_PATH=/data
VOLUME /data

# Add scripts to PATH
ENV PATH=/root/pylearn2/pylearn2/scripts:$PATH

# Set ~/pylearn2 as working directory
WORKDIR /root/pylearn2
