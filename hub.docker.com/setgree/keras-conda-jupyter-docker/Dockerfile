FROM ubuntu:18.04
LABEL maintainer='Seth Green seth@codeocean.com'

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    curl \
    bzip2 \
    ca-certificates \
    git \
  && apt-get clean  \
  && rm -rf /var/lib/apt/lists/*

RUN curl -O https://repo.continuum.io/miniconda/Miniconda3-4.5.4-Linux-x86_64.sh \
  && bash Miniconda3-4.5.4-Linux-x86_64.sh -b -p /opt/conda \
  && rm Miniconda3-4.5.4-Linux-x86_64.sh \
  && ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh \
  && echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc

RUN conda update -y conda \
  && conda install -y -c defaults -c conda-forge \
  jupyter \
  jupyterlab \
  keras \
  tensorflow \
  && conda clean --yes --all
