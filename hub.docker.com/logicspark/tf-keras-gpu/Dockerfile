FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04


RUN echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list

RUN apt-get update && apt-get -y install sudo

RUN apt-get update && apt-get install -y vim less libopencv-dev python-opencv

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        ca-certificates \
        cmake \
        wget \
        curl \
        git 

RUN useradd -ms /bin/bash ubuntu
RUN echo "ubuntu ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/ubuntu && \
    chmod 0440 /etc/sudoers.d/ubuntu

USER ubuntu
WORKDIR /home/ubuntu

ENV PYTHON_VERSION=3.6
RUN curl -o ~/miniconda.sh -O  https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh  && \
    chmod +x ~/miniconda.sh && \
    ~/miniconda.sh -b -p /home/ubuntu/conda && \
    rm ~/miniconda.sh && \
    /home/ubuntu/conda/bin/conda create -y --name py$PYTHON_VERSION python=$PYTHON_VERSION numpy pyyaml scipy \
    ipython pandas jupyter ipykernel scikit-learn && \
    /home/ubuntu/conda/bin/conda clean -ya
    
ENV PATH /home/ubuntu/conda/envs/py$PYTHON_VERSION/bin:$PATH
ENV LD_LIBRARY_PATH /home/ubuntu/conda/envs/py$PYTHON_VERSION/lib:/usr/local/cuda/lib64/:$LD_LIBRARY_PATH
    
RUN pip install --upgrade pip && \
    pip install tensorflow-gpu==1.12.0 && \
    pip install keras

RUN pip install Pillow
RUN pip install click
RUN pip install configparser
RUN pip install Flask
RUN pip install gunicorn
RUN pip install json-logging-py
RUN pip install MarkupSafe
RUN pip install olefile
RUN pip install requests
RUN pip install h5py
RUN pip install opencv-contrib-python

RUN pip install jupyterlab

ADD .jupyter /home/ubuntu/.jupyter
RUN sudo chown -R ubuntu:ubuntu /home/ubuntu/.jupyter

EXPOSE 8888
EXPOSE 5000
EXPOSE 80
