FROM continuumio/miniconda3

WORKDIR /enigma

RUN apt-get update && apt-get -y install libatlas-base-dev python-dev gfortran pkg-config libfreetype6-dev g++

COPY python3.6-environment.yml .
RUN conda env create -f python3.6-environment.yml
ENTRYPOINT [ "/bin/bash" ]


