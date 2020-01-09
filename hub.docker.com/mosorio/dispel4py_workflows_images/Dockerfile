# Create Ubuntu environment

FROM ubuntu:14.04
MAINTAINER Amy Krause <a.krause@epcc.ed.ac.uk>

RUN apt-get update && apt-get install wget curl python-dev python-pip python-setuptools git openmpi-bin openmpi-common libopenmpi-dev python3-pip -y
RUN pip3 install mpi4py
RUN pip3 install git+git://github.com/dispel4py/dispel4py.git@master
