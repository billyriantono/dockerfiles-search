FROM continuumio/miniconda3:4.5.12

# File Author / Maintainer
MAINTAINER Toni Hermoso Pulido <toni.hermoso@crg.eu> 

# https://bioconda.github.io/recipes/diamond/README.html
COPY environment.yml /
RUN conda env create -f /environment.yml && conda clean -a
ENV PATH /opt/conda/envs/diamond-conda/bin:$PATH

