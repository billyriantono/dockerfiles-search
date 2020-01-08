FROM ubuntu:latest

MAINTAINER Oscar Najera

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN apt-get -y update --fix-missing && apt-get install -y wget bzip2\
    && apt-get clean \
    && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

RUN useradd -ms /bin/bash tester
USER tester
WORKDIR /home/tester

ENV PATH /opt/conda/bin:$PATH

RUN export python_stack='numpy scipy matplotlib cython pip joblib' \
    && conda create --yes -n testpy2 python=2.7 $python_stack \
    && conda create --yes -n testpy3 python=3.6 $python_stack \
    && conda create --yes -n testpy3ob python=3.6 nomkl $python_stack \
    && conda clean --yes --all
