FROM ubuntu:16.04
MAINTAINER Nero <zhenyu707@hotmail.com>

#ARG KERAS_VERSION=2.1
#ARG TF_VERSION=1.8.0

# Supress warnings about missing front-end. As recommended at: # http://stackoverflow.com/questions/22466255/is-it-possibe-to-answer-dialog-questions-when-installing-under-docker

ARG DEBIAN_FRONTEND=noninteractive
 
# Essentials: developer tools & build tools 
RUN apt-get -y update  && apt-get install -y --no-install-recommends \
    git \
    curl \
    nano \
    unzip \
    wget \
    cmake \
    xarclock \ 
    pkg-config \
    apt-utils \
    python-imaging \
    build-essential \
    libopenblas-dev \
    libcanberra-gtk-module  \
    graphicsmagick \
    libgraphicsmagick1-dev \
    libatlas-dev \
    libavcodec-dev \
    libavformat-dev \
    libgtk2.0-dev \
    libjpeg-dev \
    liblapack-dev \
    libswscale-dev \
    && apt-get clean && rm -rf /tmp/* /var/tmp/*

#Python 3.6.6 =======================================================================

RUN apt-get install -y --no-install-recommends \
        software-properties-common && \
        add-apt-repository ppa:deadsnakes/ppa && \
        apt-get update

RUN apt-get install -y --no-install-recommends \
    python3.6 \
    python3.6-dev && \
    wget -O ~/get-pip.py \
    https://bootstrap.pypa.io/get-pip.py && \
    python3.6 ~/get-pip.py && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python3 && \
    ln -s /usr/bin/python3.6 /usr/local/bin/python && \
    python -m pip --no-cache-dir install --upgrade \
    setuptools 
#========================================================================================

# Install other useful Python packages using pip3
COPY . /root/face_recognition
RUN cd /root/face_recognition && \
    pip3 install -r require.txt 

# Expose Ports for TensorBoard (6006)
EXPOSE 6006

CMD ["/bin/bash"]
