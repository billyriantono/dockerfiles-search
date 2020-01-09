FROM continuumio/miniconda3
ENV VERSION 3.13.1 

RUN apt update && apt install -y procps && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN conda install -c bioconda spades=$VERSION && conda clean -a