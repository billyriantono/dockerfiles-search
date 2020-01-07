FROM openshine/spark-base:latest
MAINTAINER Roberto Majadas <roberto.majadas@openshine.com>

RUN apt-get update --fix-missing && \
    apt-get install -yq --no-install-recommends build-essential python-dev ca-certificates jq && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Configure environment
ENV CONDA_DIR /opt/conda
ENV PATH $CONDA_DIR/bin:$PATH

# Install conda
ENV CONDA_VERSION 4.2.12
ENV CONDA_SHA256 c59b3dd3cad550ac7596e0d599b91e75d88826db132e4146030ef471bb434e9a

RUN cd /tmp && \
    mkdir -p $CONDA_DIR && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-${CONDA_VERSION}-Linux-x86_64.sh && \
    echo "${CONDA_SHA256} *Miniconda3-${CONDA_VERSION}-Linux-x86_64.sh" | sha256sum -c - && \
    /bin/bash Miniconda3-${CONDA_VERSION}-Linux-x86_64.sh -f -b -p $CONDA_DIR && \
    rm Miniconda3-${CONDA_VERSION}-Linux-x86_64.sh && \
    $CONDA_DIR/bin/conda install --quiet --yes conda==${CONDA_VERSION} && \
    $CONDA_DIR/bin/conda config --system --add channels conda-forge && \
    $CONDA_DIR/bin/conda config --system --set auto_update_conda false && \
    conda clean -tipsy

# Install Python 3 packages
RUN conda install --yes -q \
    'notebook=4.3*' 'ipywidgets=5.2*' 'pandas=0.19*' 'numexpr=2.6*' 'matplotlib=1.5*' \
    'scipy=0.17*' 'seaborn=0.7*' 'scikit-learn=0.17*' 'scikit-image=0.11*' 'sympy=1.0*' \
    'cython=0.23*' 'patsy=0.4*' 'statsmodels=0.6*' 'cloudpickle=0.1*' 'dill=0.2*' \
    'numba=0.23*' 'bokeh=0.12*' 'sqlalchemy=1.0*' 'hdf5=1.8.17' 'h5py=2.6*' 'jsonschema' \
    'pillow' 'pip' 'jpeg=8d' 'beautifulsoup4=4.5.*' 'xlrd' \
    terminado && \
    conda clean -tipsy

# Install Python 2 packages
RUN conda create -p $CONDA_DIR/envs/python2 -q python=2.7 \
    'notebook=4.3*' 'ipywidgets=5.2*' 'pandas=0.19*' 'numexpr=2.6*' 'matplotlib=1.5*' \
    'scipy=0.17*' 'seaborn=0.7*' 'scikit-learn=0.17*' 'scikit-image=0.11*' 'sympy=1.0*' \
    'cython=0.23*' 'patsy=0.4*' 'statsmodels=0.6*' 'cloudpickle=0.1*' 'dill=0.2*' \
    'numba=0.23*' 'bokeh=0.12*' 'sqlalchemy=1.0*' 'hdf5=1.8.17' 'h5py=2.6*' 'jsonschema' \
    'pillow' 'pip' 'jpeg=8d' 'beautifulsoup4=4.5.*' 'xlrd' \
    pyzmq && \
    conda clean -tipsy
