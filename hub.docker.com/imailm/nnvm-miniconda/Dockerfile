FROM continuumio/miniconda
MAINTAINER imai@leapmind.io

RUN apt install g++ make -y
RUN pip install numpy
RUN mkdir workspace; cd workspace; \
  git clone --recursive https://github.com/dmlc/nnvm
RUN cd workspace/nnvm; make
RUN export PYTHONPATH=/workspace/nnvm/python:${PYTHONPATH}
RUN cd workspace/nnvm/python; python setup.py install --user
