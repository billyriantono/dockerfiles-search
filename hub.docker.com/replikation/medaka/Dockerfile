FROM ubuntu:xenial
MAINTAINER Christian Brandt <christian.jena@gmail.com>
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
                        wget \
                        lbzip2 \
                        zlib1g-dev \
                        bzip2 \
                        libbz2-dev
RUN apt-get clean
RUN wget --no-check-certificate https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash Miniconda3-latest-Linux-x86_64.sh -b -p /conda \
&& rm -f Miniconda3-latest-Linux-x86_64.sh
ENV PATH /conda/bin:$PATH
RUN conda config --add channels bioconda && \
		conda config --add channels conda-forge && \
		conda config --add channels default
RUN conda install medaka
