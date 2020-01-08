FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04
MAINTAINER Michal Fojtak <mfojtak@seznam.cz>
RUN apt-get update && apt-get install -y software-properties-common && add-apt-repository -y ppa:jonathonf/ffmpeg-3 && \
    apt-get update && apt-get install -y --no-install-recommends ffmpeg libavfilter-dev libavdevice-dev libavcodec-dev libav-tools x264 x265 && \
    apt-get install -y libopencv-dev python-opencv iputils-ping nano cifs-utils
########## REQUIRED DEPENDENCIES ################
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    build-essential \
    cmake \
    libprotobuf-dev \
    protobuf-compiler \
    libgoogle-glog-dev

RUN git clone --recursive https://github.com/caffe2/caffe2.git

########## OPTIONAL DEPENDENCIES ################

RUN apt-get install -y --no-install-recommends \
    libgflags-dev \
    libgoogle-glog-dev \
    libgflags-dev \
    libgtest-dev \
    libiomp-dev \
    libleveldb-dev \
    liblmdb-dev \
    libopenmpi-dev \
    libsnappy-dev \
    openmpi-bin \
    openmpi-doc \
    python-numpy \
    python-pydot \
    python-setuptools \
    python-scipy \
    wget
    
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/archive/Anaconda2-4.4.0-Linux-x86_64.sh -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /opt/conda && \
    rm ~/anaconda.sh
ENV PATH /opt/conda/bin:$PATH
RUN conda install numba bokeh accelerate
RUN pip install av opencv-python
