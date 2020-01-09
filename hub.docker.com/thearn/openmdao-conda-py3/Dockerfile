# Dockerfile for setting up OpenMDAO with MPI and PETSc with MiniConda python packages
# pyoptsparse is build and installed. 
# Defaults to running an IPython notebook server when run as a container

FROM ubuntu
LABEL maintainer="Tristan Hearn <tristan.a.hearn@nasa.gov>"

USER root

# System packages 
RUN apt-get update && apt-get install -y -y curl bzip2 openmpi-bin openmpi-doc libopenmpi-dev gfortran libblas-dev liblapack-dev libopenmpi-dev openmpi-bin git python-pip swig mercurial

# Install miniconda to /miniconda
RUN curl -LO http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash Miniconda3-latest-Linux-x86_64.sh -p /miniconda -b
RUN rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH=/miniconda/bin:${PATH}

# Python packages from conda
RUN conda install --yes python numpy scipy nose h5py mock swig cython jupyter matplotlib; conda clean -y --all;

# clone PETSc
RUN pip install mpi4py; mkdir apps; cd apps; git clone https://bitbucket.org/petsc/petsc; \
 cd petsc; \
 git checkout tags/v3.7; \
 python setup.py build install; \
 pip install git+https://bitbucket.org/petsc/petsc4py@3.7.0; \
 cd /apps; \
 rm -rf /apps/petsc; \
 curl https://gist.githubusercontent.com/thearn/96fbf920716058e59a4492ca29f86c48/raw/ > petsc_test.py; \
 mpirun --allow-run-as-root -np 2 python petsc_test.py \
 rm petsc_test.py

# Set up pyoptsparse
RUN cd apps; hg clone https://bitbucket.org/naylorb/pyoptsparse; \
 cd pyoptsparse; python setup.py build install;

# clone and install OpenMDAO
RUN pip install git+https://github.com/OpenMDAO/testflo.git; \
 cd apps; \
 git clone https://github.com/thearn/OpenMDAO; \
 cd OpenMDAO; \
 pip install -e .; 

# testflo openmdao;

# open ports for jupyter notebook
EXPOSE 8888

# create and switch to unprivileged user, keeps MPI happy
RUN useradd -ms /bin/bash user
USER user

# default start is to initialize a jupyter notebook server and wait
# run this with: docker run -v ~/:/home -it -p 8888:8888 openmdao-base
# to get a root shell instead: docker run -it --user root openmdao-base /bin/bash

CMD ["/bin/sh", "-c", "/miniconda/bin/jupyter-notebook --no-browser --ip=0.0.0.0 --notebook-dir=/home"]