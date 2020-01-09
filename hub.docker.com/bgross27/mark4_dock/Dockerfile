FROM ubuntu:16.04

ENV DEBIAN_FRONTEND=noninteractive
RUN useradd -m ubuntu

# Deps
RUN apt-get update && apt-get install -y sudo bzip2 wget htop libzmq3-dev build-essential gcc libnlopt0 curl cmake make nfs-common libgfortran3 unzip libhdf5-dev hdf5-tools git

# Anaconda
ENV CONDA="Miniconda3-latest-Linux-x86_64.sh"
RUN wget --quiet https://repo.continuum.io/miniconda/${CONDA} && /bin/bash /${CONDA} -b -p /miniconda3 && /miniconda3/bin/conda install -y jupyter

# Julia
ENV JULIA="0.5/julia-0.5.0-linux-x86_64.tar.gz"
RUN mkdir /julia && curl -L https://julialang.s3.amazonaws.com/bin/linux/x64/${JULIA} \
    | tar zxC /julia --strip-components=1 && \
    sudo -u ubuntu -H PATH="/miniconda3/bin:$PATH" /julia/bin/julia -e 'Pkg.update(); for p in["ZMQ","JSON","TimeZones","HDF5","IJulia","Distributions","SQLite","PyPlot","HypothesisTests","ParallelDataTransfer","AbstractTrees","Requests","Gumbo","OAuth","NLopt","PyCall","Nettle","ArgParse"]; Pkg.add(p); end'

RUN echo 'ubuntu ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

RUN echo 'export PATH=/julia/bin:/miniconda3/bin:/home/ubuntu/.local/bin:$PATH' >> /home/ubuntu/.bashrc

USER ubuntu

RUN git config --global credential.helper cache

RUN /miniconda3/bin/pip install --upgrade --user awscli

WORKDIR /home/ubuntu