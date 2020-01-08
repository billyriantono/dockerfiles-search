FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

ENV CUDA_HOME /usr/local/cuda

# Misc packages
RUN apt-get update
RUN apt-get install -y wget vim nano apt-utils
RUN apt-get update && apt-get install -y --no-install-recommends \
         build-essential \
         cmake \
         git \
         curl \
         vim \
         ca-certificates \
         libjpeg-dev \
         libpng-dev
RUN apt-get install -y python3 python3-dev python3-pip
RUN apt-get install -y python3-tk
RUN apt-get install -y sudo
RUN pip3 install --upgrade pip
RUN pip3 install tqdm h5py lmdb pandas
RUN pip3 install cffi
RUN pip3 install networkx scipy
RUN pip3 install scikit-image
RUN pip3 install dill
RUN pip3 install python-Levenshtein

#-----------------------------------
# Pytorch
#-----------------------------------
RUN pip3 install http://download.pytorch.org/whl/cu90/torch-0.4.0-cp35-cp35m-linux_x86_64.whl 
RUN pip3 install torchvision
RUN pip3 install git+https://github.com/pytorch/tnt.git@master
RUN pip3 install git+https://github.com/inferno-pytorch/inferno --no-deps
RUN pip3 install --upgrade pip

# Jupyter
RUN pip3 install jupyter matplotlib ipywidgets
RUN jupyter nbextension enable --py widgetsnbextension

# Pycharm
WORKDIR /home
RUN curl https://download-cf.jetbrains.com/python/pycharm-community-2017.3.4.tar.gz | tar xzv
#RUN tar xzf pycharm-community-2017.3.4.tar.gz

#RUN apt-get install -y software-properties-common python-software-properties
#RUN sh -c 'echo "deb http://archive.getdeb.net/ubuntu yakkety-getdeb apps" >> /etc/apt/sources.list.d/getdeb.list'
#RUN wget -q -O - http://archive.getdeb.net/getdeb-archive.key | apt-key add -
#RUN apt-get update
#RUN apt-get install -y pycharm
#RUN add-apt-repository ppa:ubuntu-desktop/ubuntu-make
#RUN apt-get update
#RUN apt-get install -y ubuntu-make
#RUN umake ide pycharm
#RUN apt-get -y install snap snapd
#RUN service  snapd restart
#RUN snap install pycharm-community --classic

# Tensorflow
RUN pip3 install tensorflow-gpu

RUN pip3 install --upgrade pip

#-----------------------------------
# Cleanup
#-----------------------------------

WORKDIR /workspace
