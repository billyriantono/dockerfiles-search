FROM debian:stable 

# Install important packages 
RUN apt-get update && apt-get install --fix-missing -y \ 
        python-numpy \
        python-h5py \
        python-nxs \
        python-setuptools \
        ipython \
        vim \
        git \
        wget \
        gcc \
        g++

# Install jdk needed by scipion 
RUN echo "deb http://ftp.debian.org/debian jessie-backports main" | tee -a /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y -t jessie-backports \
        openjdk-8-jdk \
        ca-certificates-java

# Install dependencies needed by scipion 
RUN apt-get install -y \
        cmake \
        libopenmpi-dev \
        openmpi-bin \
        gfortran \
        libxft-dev \
        libssl-dev \
        libxext-dev \
        libxml2-dev \
        libreadline6 \
        libquadmath0 \
        libxslt1-dev \
        libxss-dev \
        libgsl0-dev \
        libx11-dev \
        libfreetype6-dev

# Install scipion WORKDIR "/home"
WORKDIR "/home"
RUN wget http://scipion.cnb.csic.es/m/static/install/scipion_v1.0.1_2016-06-30_linux64.tgz
RUN tar -xvzf scipion_v1.0.1_2016-06-30_linux64.tgz
WORKDIR "/home/scipion"
RUN ./scipion config
RUN rm -rf sofware/tmp/*
RUN rm -rf sofware/em/*.tgz

# Export Path to allow running scipion 
RUN export PATH=$PATH:/home/scipion/


