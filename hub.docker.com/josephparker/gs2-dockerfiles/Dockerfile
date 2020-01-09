FROM ubuntu:18.04

RUN apt update
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:ubuntu-toolchain-r/test \
    && apt update \ 
    && apt-get install -y \
    gcc-8 g++-8 gfortran-8 
RUN update-alternatives --install /usr/bin/gfortran gfortran /usr/bin/gfortran-8 0 \
    && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 0 \
    && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 0
RUN update-alternatives --config gfortran \
    && update-alternatives --config gcc \
    && update-alternatives --config g++
RUN gcc --version
RUN gfortran --version
RUN apt install -y \
    mpich libmpich-dev \
    libnetcdf-dev \
    libnetcdff-dev \
    libfftw3-dev \
    netcdf-bin
RUN apt install -y \
    git
RUN apt install -y \
    curl
RUN mpif90 --version
# Create dirs and users
RUN mkdir -p /opt/atlassian/bitbucketci/agent/build \
    && sed -i '/[ -z \"PS1\" ] && return/a\\ncase $- in\n*i*) ;;\n*) return;;\nesac' /root/.bashrc \
    && useradd --create-home --shell /bin/bash --uid 1000 pipelines
WORKDIR /opt/atlassian/bitbucketci/agent/build
ENTRYPOINT /bin/bash
