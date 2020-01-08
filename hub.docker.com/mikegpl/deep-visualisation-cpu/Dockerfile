FROM ubuntu:18.04

WORKDIR /home

ARG DEBIAN_FRONTEND=noninteractive

RUN sed -Ei 's/^# deb-src /deb-src /' /etc/apt/sources.list
RUN apt-get update
RUN apt build-dep caffe-cpu -y 
RUN apt-get install ca-certificates -y
RUN apt install libhdf5-serial-dev
RUN apt-get install hdf5-tools
WORKDIR /usr/lib/x86_64-linux-gnu/
RUN ln -s libhdf5_serial.so.8.0.2 libhdf5.so
RUN apt install libblas-dev liblapack-dev libatlas-base-dev
RUN apt install python-opencv python-skimage -y
RUN ldconfig

WORKDIR /home
RUN git clone https://github.com/BVLC/caffe.git
WORKDIR /home/caffe

COPY Makefile.config /home/caffe

RUN git remote add yosisnski https://github.com/yosinski/caffe.git
RUN git fetch --all
RUN git checkout deconv-deep-vis-toolbox
RUN make clean && make && make -j pycaffe

WORKDIR /home
RUN git clone https://github.com/yosinski/deep-visualization-toolbox