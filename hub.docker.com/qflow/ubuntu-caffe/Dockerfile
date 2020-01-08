FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04
MAINTAINER Michal Fojtak <mfojtak@seznam.cz>
WORKDIR /workspace
RUN apt update && apt install -y build-essential cmake git autoconf automake libtool curl make g++ unzip && \
    apt install -y libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev libssl-dev && \
    apt install -y libgflags-dev libgoogle-glog-dev liblmdb-dev python-numpy && \
    apt install -y --no-install-recommends libboost-all-dev libatlas-base-dev && \
    git clone --branch v3.2.0 https://github.com/google/protobuf.git

WORKDIR /workspace/protobuf
RUN ./autogen.sh && ./configure && make install && ldconfig
WORKDIR /workspace
RUN rm -r protobuf && git clone --branch rc4 https://github.com/BVLC/caffe.git && mkdir caffe/build
WORKDIR /workspace/caffe/build
RUN cmake -DUSE_CUDNN=1 .. && make -j"$(nproc)"
ENV CAFFE_ROOT=/workspace/caffe
ENV PATH $CAFFE_ROOT/build/tools:$PATH
RUN echo "$CAFFE_ROOT/build/lib" >> /etc/ld.so.conf.d/caffe.conf && ldconfig

WORKDIR /workspace
