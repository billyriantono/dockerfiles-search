FROM ubuntu:14.04
MAINTAINER Artanis <283186127@qq.com>

# Ubuntu 14.04 with CUDA 7.0 installed

RUN mv /etc/apt/sources.list /etc/apt/sources.list.backup

RUN echo "\
deb http://mirrors.163.com/ubuntu/ trusty main restricted universe multiverse\n \
deb http://mirrors.163.com/ubuntu/ trusty-security main restricted universe multiverse\n \
deb http://mirrors.163.com/ubuntu/ trusty-updates main restricted universe multiverse\n \
deb http://mirrors.163.com/ubuntu/ trusty-proposed main restricted universe multiverse\n \
deb http://mirrors.163.com/ubuntu/ trusty-backports main restricted universe multiverse\n \
deb-src http://mirrors.163.com/ubuntu/ trusty main restricted universe multiverse\n \
deb-src http://mirrors.163.com/ubuntu/ trusty-security main restricted universe multiverse\n \
deb-src http://mirrors.163.com/ubuntu/ trusty-updates main restricted universe multiverse\n \
deb-src http://mirrors.163.com/ubuntu/ trusty-proposed main restricted universe multiverse\n \
deb-src http://mirrors.163.com/ubuntu/ trusty-backports main restricted universe multiverse\n" > /etc/apt/sources.list

RUN apt-get update && \
  apt-get install -q -y build-essential aria2 vim

# Change to the /tmp directory
RUN cd /opt && \
# Download run file
  aria2c -x 16 -s 16 -j 16 http://developer.download.nvidia.com/compute/cuda/7_0/Prod/local_installers/cuda_7.0.28_linux.run && \
# Make the run file executable and extract
  chmod +x cuda_*_linux.run && ./cuda_*_linux.run -extract=`pwd` && \
# Install CUDA drivers (silent, no kernel)
  ./NVIDIA-Linux-x86_64-*.run -s --no-kernel-module && \
# Install toolkit (silent)  
  ./cuda-linux64-rel-*.run -noprompt && \
# Install samples (silent)
  ./cuda-samples-linux-*.run -noprompt -cudaprefix=/usr/local/cuda/

# Add to path
ENV PATH /usr/local/cuda/bin:${PATH}
# Configure dynamic link
RUN echo "/usr/local/cuda/lib64" >> /etc/ld.so.conf && ldconfig
