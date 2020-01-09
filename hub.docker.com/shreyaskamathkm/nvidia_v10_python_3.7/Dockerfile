FROM nvidia/cuda:10.2-cudnn7-runtime-ubuntu16.04
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils \
         build-essential \
	 wget \
         cmake \
         git \
         curl \
         vim \
         ca-certificates \
         libjpeg-dev \
         libpng-dev &&\
     rm -rf /var/lib/apt/lists/*


RUN wget --quiet https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh -O ~/anaconda.sh && \
    /bin/bash ~/anaconda.sh -b -p /opt/conda && \
    rm ~/anaconda.sh

RUN /opt/conda/bin/conda update -y --all && \
    /opt/conda/bin/conda clean -ya

ENV PATH /opt/conda/bin:$PATH

# This must be done before pip so that requirements.txt is available

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

WORKDIR /workspace
RUN chmod -R a+w /workspace
