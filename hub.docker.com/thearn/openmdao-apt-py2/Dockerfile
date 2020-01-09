# Dockerfile for setting up OpenMDAO with python 2 (no MPI or pyopt)
# Ubuntu system packages (apt-get) are used

FROM ubuntu
LABEL maintainer="Tristan Hearn <tristan.a.hearn@nasa.gov>"

# System packages 
RUN apt-get update && apt-get install -y \
	python-numpy \
	python-scipy \
	python-matplotlib \
	python-pip \
	git \
	libhdf5-serial-dev \
	python-h5py \
	python

# clone and install OpenMDAO
RUN pip install git+https://github.com/OpenMDAO/testflo.git; \
 mkdir apps; cd apps; \
 git clone https://github.com/thearn/OpenMDAO; \
 cd OpenMDAO; \
 pip install -e .; 

RUN cd apps/OpenMDAO/openmdao; testflo .


# create and switch to unprivileged user
RUN useradd -ms /bin/bash user
USER user