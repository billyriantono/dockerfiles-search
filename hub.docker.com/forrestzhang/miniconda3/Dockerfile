FROM ubuntu:16.04

MAINTAINER Tao Zhang "forrestzhang1982@gmail.com"

RUN apt-get update && apt-get install -y curl build-essential
RUN apt-get install -y language-pack-en
RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

RUN curl -LO http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh

RUN bash Miniconda3-latest-Linux-x86_64.sh -p /opt/miniconda -b
RUN rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH=/opt/miniconda/bin:${PATH}
RUN conda update -y conda
