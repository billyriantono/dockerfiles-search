FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

USER root:root
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && \
    apt-get install -y wget bzip2 gcc g++ make

# Install Miniconda

ENV PATH /opt/miniconda/bin:$PATH

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.5.11-Linux-x86_64.sh -O /tmp/miniconda.sh && \
    /bin/bash /tmp/miniconda.sh -bf -p /opt/miniconda && \
    conda clean -ay && \
    rm /tmp/miniconda.sh

# Install Open MPI

RUN wget -q https://www.open-mpi.org/software/ompi/v1.10/downloads/openmpi-1.10.4.tar.gz && \
    tar -xzf openmpi-1.10.4.tar.gz && \
    cd openmpi-1.10.4 && \
    ./configure --prefix=/usr/local/mpi && \
    make -j"$(nproc)" install && \
    cd .. && \
    rm -rf /openmpi-1.10.4 && \
    rm -rf openmpi-1.10.4.tar.gz

ENV PATH=/usr/local/mpi/bin:$PATH \
    LD_LIBRARY_PATH=/usr/local/mpi/lib:$LD_LIBRARY_PATH

# Set Path for Non-Interactive Execution

RUN sed -i '1s/^/LD_LIBRARY_PATH="\/usr\/local\/mpi\/lib:$LD_LIBRARY_PATH"\n\n/' ~/.bashrc

RUN sed -i '1s/^/PATH="\/usr\/local\/mpi\/bin:$PATH"\n\n/' ~/.bashrc
