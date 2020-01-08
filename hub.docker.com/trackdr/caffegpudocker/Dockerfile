# Start with CUDA base image
FROM kaixhin/cuda
MAINTAINER me

# Install git, bc and dependencies
RUN apt-get update && apt-get install -y \
  git \
  bc \
  libatlas-base-dev \
  libatlas-dev \
  libboost-all-dev \
  libprotobuf-dev \
  libgoogle-glog-dev \
  libgflags-dev \
  protobuf-compiler \
  libhdf5-dev \
  libleveldb-dev \
  liblmdb-dev \
  libsnappy-dev \
  python-pip \
  python-dev \
  python-numpy \
  python-scipy \
  libopencv-dev
  
# Clone Caffe repo and move into it
RUN cd /opt && git clone https://github.com/BVLC/caffe.git && cd caffe
RUN cd /opt/caffe/python && for req in $(cat requirements.txt); do pip install $req; done  
RUN cd /opt/caffe && cp Makefile.config.example Makefile.config
RUN cd /opt/caffe && sed -i '/^# WITH_PYTHON_LAYER := 1/s/^# //' Makefile.config
RUN cd /opt/caffe && make all
RUN cd /opt/caffe && make pycaffe
RUN cd /opt/caffe && make test

ENV PYTHONPATH /opt/caffe/python:$PYTHONPATH

