FROM continuumio/miniconda3
ENV VERSION 2.17 

RUN apt update && apt install -y procps && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN conda config --add channels conda-forge && \
    conda config --add channels bioconda && \
    conda config --add channels default

RUN conda install minimap2=$VERSION samtools=1.9 && conda clean -a
