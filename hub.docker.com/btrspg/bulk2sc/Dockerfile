FROM continuumio/miniconda3:latest
MAINTAINER CHEN,Yuelong <yuelong.chen.btr@gmail.com>

ARG conda_forge='python=3.7.3 libopenblas libiconv'
ARG r='r'
ARG bioconda='bioconductor-affy java-jdk \
    bioconductor-annotate bioconductor-org.Hs.eg.db bioconductor-sva bioconductor-limma \
    r-pamr bioconductor-bladderbatch bioconductor-hgu133a.db bioconductor-hgu133b.db \
    bioconductor-hgu133plus2.db bioconductor-hgu133acdf \
    bioconductor-hgu133bcdf bioconductor-hgu133plus2cdf'



USER root
ENV PATH /opt/bin:/opt/conda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:$PATH
RUN conda install -y -c r $r \
    && conda install -y -c conda-forge $conda_forge \
    && conda install -y -c bioconda $bioconda

RUN pip install git+https://github.com/btrspg/bioplots.git

RUN mkdir -p /opt/bin /opt/database
COPY DockerEnv/database/ /opt/database
COPY DockerEnv/CIBERSORT /opt/bin/
COPY rscripts/* /opt/bin/
COPY shscripts/* /opt/bin/


CMD bash





