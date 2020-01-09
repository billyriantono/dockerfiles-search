FROM continuumio/miniconda3:4.6.14
MAINTAINER Sangram Keshari Sahu <sangramsahu15@gmail.com>

RUN apt-get update \
	&& apt-get install -y procps \
	&& apt-get clean -y \
	&& conda install conda=4.6.7

COPY env.yml /
RUN conda env create -f env.yml && conda clean -a \
	&& echo "source activate $(head -1 env.yml | cut -d' ' -f2)" > ~/.bashrc \
ENV PATH /opt/conda/envs/$(head -1 env.yml | cut -d' ' -f2)/bin:$PATH
