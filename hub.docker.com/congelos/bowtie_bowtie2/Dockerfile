#Use an official Ubuntu runtime as a parent image
FROM ubuntu:latest

#MAINTAINER ConYel <https://github.com/ConYel>

# Set the working directory to /home
WORKDIR /home

#set User ROOT
USER root

# config issues about region and time 
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

RUN apt-get update -y \
	&& apt-get install -y --no-install-recommends \
	build-essential \
	software-properties-common \
	apt-utils \
	nano \
	git \
	python \
        unzip \
        wget \   
	locales \
	&& locale-gen en_US.UTF-8 \
	&& wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh \
	&& bash ~/miniconda.sh -b -p ~/miniconda \
	&& rm ~/miniconda.sh \
	&& echo 'export PATH="~/miniconda/bin:$PATH"' >> ~/.bashrc \
	&& ln -sf ~/miniconda/condabin/conda /usr/local/bin/conda \
	&& rm -rf /var/lib/apt/lists/* /tmp/* 
        
RUN conda update conda \
	&& conda config --add channels defaults \
	&& conda config --add channels bioconda \
	&& conda config --add channels conda-forge \
	&& conda install bowtie bowtie2  -y
