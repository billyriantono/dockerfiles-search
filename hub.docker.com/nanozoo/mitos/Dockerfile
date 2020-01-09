FROM continuumio/miniconda3
ENV VERSION 2.0.3

RUN apt update && apt install -y procps && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN conda config --add channels conda-forge && \
    conda config --add channels bioconda && \
    conda config --add channels default

RUN conda install python=2.7 mitos=$VERSION bioawk=1.0 && conda clean -a