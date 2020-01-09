FROM continuumio/miniconda3
ENV VERSION 4.8.1 

RUN useradd --create-home nanozoo
WORKDIR /home/nanozoo

RUN conda config --add channels conda-forge && \
    conda config --add channels bioconda && \
    conda config --add channels default

RUN conda install cd-hit=$VERSION && conda clean -a

USER nanozoo
