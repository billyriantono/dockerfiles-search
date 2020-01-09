FROM continuumio/miniconda3:latest

ARG PYTHON_VERSION=3.6

# Add version file "version.txt" to the project
ADD version.txt .

# Update conda config
RUN conda config --set always_yes yes
RUN conda update -q conda

# Create the conda environment. The main test environment.
RUN conda create -q -n test-environment python=$PYTHON_VERSION

# List all installed packages
RUN /bin/bash -c 'source activate test-environment && python --version && conda env list && pip list'

# Create more environments
RUN conda create -q -n py27 -c conda-forge python=2.7
RUN conda create -q -n py34 -c conda-forge python=3.4
RUN conda create -q -n py35 -c conda-forge python=3.5
RUN conda create -q -n py36 -c conda-forge python=3.6
RUN conda create -q -n py37 -c conda-forge python=3.7

