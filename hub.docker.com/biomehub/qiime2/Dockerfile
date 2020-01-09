FROM continuumio/miniconda3:latest
ENV DEBIAN_FRONTEND noninteractive
MAINTAINER BiomeHub

LABEL version="2019.10"
LABEL software.version="2019.10"
LABEL software="qiime2"

COPY qiime2-2019.10-py36-linux-conda.yml ./

RUN conda env create -f qiime2-2019.10-py36-linux-conda.yml

RUN echo "source activate qiime2-2019.10" > ~/.bashrc

ENV PATH /opt/conda/envs/qiime2-2019.10/bin:$PATH
ENV export LC_ALL=C.UTF-8
ENV export LANG=C.UTF-8
 
