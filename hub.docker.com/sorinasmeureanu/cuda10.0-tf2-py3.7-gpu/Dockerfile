# TensorFlow 2.0, Python3.7, cuda and cuDNN (GPU) 
# and some extra packages (opencv, scipy, sklearn, etc)

FROM nvidia/cuda:10.0-cudnn7-runtime-ubuntu16.04

USER root

# install packages
RUN apt-get update -qq \
 && apt-get install -y --no-install-recommends\
    software-properties-common \
    gcc \
	g++\
	wget\
	make \
	zlib1g \
	zlib1g-dev \
	build-essential \
	openssl \
	curl \
	libssl-dev \
	libffi-dev \
	libsqlite3-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
 
# install python 3.7.5
RUN wget https://www.python.org/ftp/python/3.7.5/Python-3.7.5.tgz  
RUN tar -xvf Python-3.7.5.tgz  
RUN cd Python-3.7.5 \
	&& ./configure --enable-loadable-sqlite-extensions \
	&& make \
	&& make install

# install pip3
RUN curl https://bootstrap.pypa.io/get-pip.py | python3

# install numpy
RUN python3.7 -m pip install numpy

# install tensorflow 2.0
# RUN pip3 install tensorflow-gpu==2.0
RUN pip3 install tensorflow-gpu

# install opencv, ...
RUN apt update && apt install -y libsm6 libxext6 libxrender-dev
RUN pip3 install opencv-python
RUN pip3 install scipy
RUN pip3 install sklearn

# create a link to use python3 as as 'python'
RUN ln -s /usr/local/bin/python3 /usr/bin/python

WORKDIR /code/