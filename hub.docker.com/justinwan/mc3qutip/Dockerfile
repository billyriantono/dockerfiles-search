FROM continuumio/miniconda3:latest

ARG PYTHON_VERSION=3.6

# Add version file "version.txt" to the project
ADD version.txt .

# Add gcc
RUN apt-get update
RUN apt-get install --yes --no-install-recommends gcc
RUN apt-get install --yes build-essential

# Update conda config
RUN conda config --set always_yes yes
RUN conda update -q conda

## Create the conda environment "test-environment"
RUN conda create -q -n test-environment python=$PYTHON_VERSION

# Activate test-environment
RUN /bin/bash -c 'source activate test-environment && conda env list'

# Upgrade pip
RUN /bin/bash -c 'source activate test-environment && pip install --upgrade pip'

# Add packages for unittest
RUN /bin/bash -c 'source activate test-environment && pip install nose coverage nosexcover nose-cov xenon'

# Install scientific packages
RUN /bin/bash -c 'source activate test-environment && pip install numpy scipy matplotlib cython'

# Install qutip
RUN /bin/bash -c 'source activate test-environment && pip install qutip'

# List all installed packages
RUN /bin/bash -c 'source activate test-environment && python --version && conda env list && pip list'
