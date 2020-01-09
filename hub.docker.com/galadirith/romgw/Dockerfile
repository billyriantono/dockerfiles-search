FROM python:2-jessie
MAINTAINER Edward Fauchon-Jones <edward.fauchon.jones@gmail.com>

# Install system dependencies
RUN apt-get update -yqqq && apt-get install -y \
    libgsl0-dev \
    libgsl0ldbl \
    libfftw3-dev \
    swig3.0 \
 && rm -rf /var/lib/apt/lists/*

# Install python dependencies
RUN pip install --no-cache-dir \
    numpy \
    scipy \
    h5py \
    matplotlib \
    jupyter \
    jupyterlab \
    lalsuite \
    pandas \
    seaborn \
    emcee \
    corner \
    futures \
    sklearn \
    git+https://github.com/llondon6/positive.git \
    tensorflow \
    keras

# Clone non installable python packages
RUN cd /opt \
 && git clone https://bitbucket.org/chadgalley/romspline.git
RUN cd /opt \
 && git clone https://bitbucket.org/chadgalley/rompy.git
ENV PYTHONPATH "/opt/"

# Build installable python package and install
RUN mkdir /src
RUN cd /src \
 && git clone https://github.com/mpuerrer/TPI.git \
 && cd TPI \
 && python setup.py build_ext \
 && python setup.py install \
 && cd .. \
 && rm -rf TPI
RUN cd /src \
 && git clone https://github.com/moble/GWFrames.git \
 && cd GWFrames \
 && git submodule init \
 && git submodule update \
 && cd Code \
 && ln -s /usr/bin/swig3.0 /usr/bin/swig \
 && python setup.py install \
 && cd .. \
 && rm -rf GWFrames
