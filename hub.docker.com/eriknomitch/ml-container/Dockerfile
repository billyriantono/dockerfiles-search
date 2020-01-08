# ================================================
# DOCKERFILE->ML-CONTAINER =======================
# ================================================
FROM nvidia/cuda:10.0-base-ubuntu18.04

MAINTAINER Erik Nomitch <erik@nomitch.com>

ENV LANG C.UTF-8
ENV DEBIAN_FRONTEND noninteractive

ENV PYTHON_VERSION=3.6
ENV PATH /usr/local/bin:$PATH
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64

LABEL com.nvidia.volumes.needed="nvidia_driver"

# ------------------------------------------------
# NVIDIA-REPO ------------------------------------
# ------------------------------------------------
RUN apt-get update && apt-get install -y --no-install-recommends \
      apt-transport-https \
      apt-utils \
      curl \
      wget

RUN wget -qO - https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub | apt-key add -

RUN echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list

# ------------------------------------------------
# PACKAGES->SYSTEM -------------------------------
# ------------------------------------------------
RUN apt-get update && apt-get install -y --no-install-recommends \
      build-essential \
      ca-certificates \
      git \
      vim \
      zip \
      unzip \
      python-qt4 \
      libjpeg-dev \
      libpng-dev \
      cmake \
      htop \
      tmux &&\
      rm -rf /var/lib/apt/lists/* \
             /etc/apt/sources.list.d/nvidia-ml.list

# ------------------------------------------------
# CONDA ------------------------------------------
# ------------------------------------------------
RUN curl -o ~/miniconda.sh -O  https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh  && \
     chmod +x ~/miniconda.sh && \
     ~/miniconda.sh -b -p /opt/conda && \
     rm ~/miniconda.sh && \
     /opt/conda/bin/conda install conda-build

ENV PATH=$PATH:/opt/conda/bin/

# ------------------------------------------------
# USER -------------------------------------------
# ------------------------------------------------
# ENV USER ml

# Create 'ml' Conda environment
COPY environment.yaml /environment.yaml
RUN conda env create -f /environment.yaml
RUN conda init bash

WORKDIR /notebooks

# Activate Source
CMD source ~/.bashrc
CMD conda activate ml

# ------------------------------------------------
# NOTEBOOKS --------------------------------------
# ------------------------------------------------
RUN chmod -R a+w /notebooks
WORKDIR /notebooks

# ------------------------------------------------
# PAPERSPACE -------------------------------------
# ------------------------------------------------
COPY config.yaml /root/.root/config.yaml
COPY config.yaml /root/config.yaml

# ------------------------------------------------
# RUN --------------------------------------------
# ------------------------------------------------
COPY run.sh /run.sh

# ------------------------------------------------
# CLEANUP ----------------------------------------
# ------------------------------------------------
RUN ldconfig && \
    apt-get clean && \
    apt-get autoremove

# ------------------------------------------------
# COMMAND ----------------------------------------
# ------------------------------------------------
CMD ["/run.sh"]
