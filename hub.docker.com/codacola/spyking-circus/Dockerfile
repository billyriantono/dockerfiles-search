FROM continuumio/miniconda3:latest

RUN apt-get update && apt-get -y install gcc

RUN conda install mpi4py numpy cython scipy matplotlib h5py setuptools colorama blosc

WORKDIR /app

RUN ls

RUN git clone https://github.com/codacola/spyking-circus.git spyking-circus

WORKDIR /app/spyking-circus

RUN pip install .

WORKDIR /

