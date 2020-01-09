# Dockerfile for setting up OpenMDAO with python 3 (no MPI)
# Ubuntu system packages (apt-get) are used
# Defaults to running an IPython notebook server when run as a container

FROM ubuntu
LABEL maintainer="Tristan Hearn <tristan.a.hearn@nasa.gov>"

# System packages 
RUN apt-get update && apt-get install -y \
	python3-numpy \
	python3-scipy \
	python3-matplotlib \
	python3-pip \
	git \
	libhdf5-serial-dev \
	python3-h5py \
	python

# clone and install OpenMDAO
RUN pip3 install jupyter git+https://github.com/OpenMDAO/testflo.git; \
 mkdir apps; cd apps; \
 git clone https://github.com/thearn/OpenMDAO; \
 cd OpenMDAO; \
 pip3 install -e .; testflo openmdao;

# open ports for jupyter notebook
EXPOSE 8888

# create and switch to unprivileged user
RUN useradd -ms /bin/bash user
USER user

# default start is to initialize a jupyter notebook server and wait
# run this with: docker run -v ~/:/home -it -p 8888:8888 openmdao-base
# to get a root shell instead: docker run -it --user root openmdao-base /bin/bash

CMD ["/bin/sh", "-c", "/miniconda/bin/jupyter-notebook --no-browser --ip=0.0.0.0 --notebook-dir=/home"]