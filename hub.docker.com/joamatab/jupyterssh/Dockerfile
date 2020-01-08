FROM jupyter/datascience-notebook:2ce7c06a61a1
USER root
RUN apt-get update && apt install -y \
    openssh-client \
    rsync \
    vim \
    iputils-ping
RUN conda create -n mp -c conda-forge pymeep -y
USER jovyan
RUN mkdir -p ~/.pip
COPY pip.conf /home/jovyan/.pip/pip.conf

