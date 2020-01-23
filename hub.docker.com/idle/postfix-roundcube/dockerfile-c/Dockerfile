# Start with the Ubuntu base image.
FROM ubuntu:14.04
MAINTAINER Ahmed S. Kaseb <akaseb@purdue.edu>

# Install wget.
RUN apt-get install -y wget

# Install CUDA 7.0.28.
RUN cd /tmp && \
    wget http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1404/x86_64/cuda-repo-ubuntu1404_7.0-28_amd64.deb && \
    dpkg -i cuda-repo-ubuntu1404_*_amd64.deb && \
    apt-get update && \
    apt-get install -y --no-install-recommends cuda

# Add the CUDA binaries to PATH.
ENV PATH /usr/local/cuda/bin:${PATH}

# Configure the dynamic linker run-time bindings.
RUN echo "/usr/local/cuda/lib64" >> /etc/ld.so.conf && ldconfig
