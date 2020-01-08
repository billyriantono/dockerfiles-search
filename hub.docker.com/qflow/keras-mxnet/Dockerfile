FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04
MAINTAINER Michal Fojtak <mfojtak@seznam.cz>
RUN apt-get update && apt-get install -y software-properties-common && \
    apt-get install -y iputils-ping \
    nano \
    wget \
    libgtk2.0-0 \
    git \
    build-essential \
    cmake \
    libprotobuf-dev \
    protobuf-compiler \
    libgoogle-glog-dev \
    fonts-dejavu \
    gfortran \
    apt-transport-https \
    unzip \
    libaio1 \
    libgl1-mesa-glx \
    libx264-dev libvpx-dev yasm \
    gcc curl && apt-get clean && \
    rm -rf /var/lib/apt/lists/*



RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /opt/conda && \
    rm ~/anaconda.sh
ENV PATH /opt/conda/bin:$PATH

RUN pip install  mxnet-cu90 keras-mxnet
RUN conda install --yes numba bokeh libgcc wget && \
    conda install --yes -c conda-forge pika av && \
    conda install --yes -c anaconda tornado && \
    conda install --yes -c menpo opencv3 && \
    conda install --yes -c numba pyculib
ADD jupyter_notebook_config.py /root/.jupyter/

ADD start.sh /start.sh
RUN chmod +x /start.sh
EXPOSE 8888
ENTRYPOINT ["/start.sh"]
