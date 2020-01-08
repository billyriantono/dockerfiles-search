FROM debian:latest
MAINTAINER Antoine Henning <henning.antoine@gmail.com>

# Get dependencies
RUN apt-get update -qq && apt-get install -y \
        git \
        build-essential gcc gfortran pkg-config \
        python2.7 python-setuptools python-dev python-pip python-numpy python-scipy python-matplotlib python-pandas python-sympy python-nose ipython ipython-notebook \
        libhdf5-dev libfreetype6-dev liblapack-dev && \
    rm -rf /var/lib/apt/lists/* && \
    pip install --upgrade scikit-learn && \
    pip install --upgrade h5py

# Installation
RUN mkdir /vmaf 
WORKDIR /vmaf
RUN git clone https://github.com/Netflix/vmaf . && \
    make
ENV PYTHONPATH=/vmaf/python:$PYTHONPATH

# Testing
RUN ./unittest

CMD ["bash"]
