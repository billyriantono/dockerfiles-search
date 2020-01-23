FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu16.04
ARG PYTHON_VERSION=3.6
ARG WITH_TORCHVISION=1
RUN apt-get update && apt-get install -y --no-install-recommends \
         build-essential \
         cmake \
         git \
         curl \
         ca-certificates \
	 wget \
         libjpeg-dev \
	 ffmpeg \
         libpng-dev && \
     rm -rf /var/lib/apt/lists/*


RUN curl -o ~/miniconda.sh -O  https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh  && \
     chmod +x ~/miniconda.sh && \
     ~/miniconda.sh -b -p /opt/conda && \
     rm ~/miniconda.sh && \
     /opt/conda/bin/conda clean -ya
ENV PATH /opt/conda/bin:$PATH
# This must be done before pip so that requirements.txt is available
WORKDIR /opt/pytorch
COPY . .

WORKDIR /workspace

RUN wget https://raw.githubusercontent.com/chahuja/dockers/master/pytorch/env.yml
SHELL ["/bin/bash", "-c"]
RUN conda env create -n torch -f env.yml
RUN rm env.yml
RUN echo "source activate torch" > ~/.bashrc
#ENV PATH /opt/conda/envs/torch/bin:$PATH

RUN chmod -R a+w .