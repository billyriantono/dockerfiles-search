################################################################
# Dockerfile to build container images for RNA-seq pipeline
# including hisat2, sratools, samtools, stringtie and gffcompare
# Based on Ubuntu
################################################################

FROM rocker/tidyverse:3.4.2

# File Author / Maintainer
MAINTAINER Ania Tassinari <ania.tassinari@agios.com>

# install dependencies first
RUN apt-get update  && apt-get install -y \
    build-essential \
    gcc-multilib \
    zlib1g-dev \
    curl \
    wget \
    cmake \
    python \
    python-pip \
    python-dev \
    python2.7-dev \
    python-numpy \
    python-matplotlib \
    hdf5-tools \
    libhdf5-dev \
    hdf5-helpers \
    libhdf5-serial-dev \
    libssh2-1-dev \
    libcurl4-openssl-dev \
    icu-devtools \
    libssl-dev \
    libxml2-dev \
    r-bioc-biobase \
    git \
    apt-utils \
    pigz \
    default-jre



# Install stringtie
WORKDIR /docker
RUN wget http://ccb.jhu.edu/software/stringtie/dl/stringtie-1.3.3b.Linux_x86_64.tar.gz && \
    tar zxf stringtie-1.3.3b.Linux_x86_64.tar.gz && \
    cp ./stringtie-1.3.3b.Linux_x86_64/stringtie /usr/bin/
    
# Download stringtie prepDE
WORKDIR /docker
RUN wget http://ccb.jhu.edu/software/stringtie/dl/prepDE.py
    

RUN rm -rf /docker/stringtie-1.3.3b.Linux_x86_64
RUN apt-get clean
RUN apt-get remove --yes --purge build-essential gcc-multilib apt-utils zlib1g-dev vim

# Set default working path
WORKDIR /docker
