FROM continuumio/miniconda3:4.6.14
MAINTAINER Sangram Keshari Sahu <sangramsahu15@gmail.com>

RUN apt-get update \
	&& apt-get install -y procps \
	&& apt-get clean -y \
	&& conda install conda=4.6.7 \
	&& mkdir conda_env_files

COPY envs/* /env_files/
RUN conda env create -f /env_files/environment.yml && conda clean -a \
	&& echo "source activate $(head -1 /env_files/environment.yml | cut -d' ' -f2)" > ~/.bashrc \
	&& conda env create -f /env_files/diffexp.yml && conda clean -a \
	&& echo "source activate $(head -1 /env_files/diffexp.yml | cut -d' ' -f2)" > ~/.bashrc \
	&& conda env create -f /env_files/sample_check.yml && conda clean -a \
	&& echo "source activate $(head -1 /env_files/sample_check.yml | cut -d' ' -f2)" > ~/.bashrc \
	&& conda env create -f /env_files/sig_bio.yml && conda clean -a \
	&& echo "source activate $(head -1 /env_files/sig_bio.yml | cut -d' ' -f2)" > ~/.bashrc \
	&& conda env create -f /env_files/summary.yml && conda clean -a \
	&& echo "source activate $(head -1 /env_files/summary.yml | cut -d' ' -f2)" > ~/.bashrc