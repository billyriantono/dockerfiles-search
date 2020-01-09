FROM rocker/r-ver:3.2.0

MAINTAINER Gustavo F. Bayon <fernandezgustavo@uniovi.es>

RUN . /etc/environment && \
  apt-get update && \
  apt-get install -y python3 python3-setuptools python3-dev build-essential && \
  easy_install3 pip && \
  pip install snakemake==3.5.4

RUN apt-get install -y libreadline-dev libpcre3-dev libz-dev libicu-dev \
  liblzma-dev libbz2-dev && \
  pip install rpy2==2.6.2
 
RUN echo "/usr/local/lib/R/lib/" > /etc/ld.so.conf.d/libR.conf && ldconfig



