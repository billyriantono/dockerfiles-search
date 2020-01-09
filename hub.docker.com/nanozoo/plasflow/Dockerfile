FROM ubuntu:bionic
ENV VERSION 1.1.0 

ENV DEBIAN_FRONTEND=noninteractive
RUN useradd --create-home nanozoo
WORKDIR /home/nanozoo

RUN apt-get update && apt-get install -y --no-install-recommends \
					 wget
RUN apt-get clean

# install correct conda version for plasflow
RUN wget --no-check-certificate https://repo.continuum.io/miniconda/Miniconda3-4.5.11-Linux-x86_64.sh
RUN bash Miniconda3-4.5.11-Linux-x86_64.sh -b -p /conda && rm -f Miniconda3-4.5.11-Linux-x86_64.sh

ENV PATH /conda/bin:$PATH
# install plasflow
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge
RUN conda install plasflow=$VERSION -c smaegol
RUN conda install -c bioconda perl-bioperl perl-getopt-long && conda clean -a 
# modify shebangs for bioperl
RUN sed -i '1i#!/conda/bin/perl' /conda/bin/filter_sequences_by_length.pl

USER nanozoo
