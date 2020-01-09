##########################
# Docker Machine Structure:
# + programs --> /opt: anaconda3, ...
# + workdir  --> /ws: bin, media (disks into host), logs, project (scripts, data - dataset, experiments, preprocessing, sources, bin)
# + expose: 12350 (jupyter-lab), 6006 (tensorboard)
##########################

FROM nvidia/cuda:10.0-cudnn7-runtime-ubuntu18.04

###################################
# Add common Linux dependencies
###################################
RUN apt-get clean && apt-get update -y -qq
RUN apt-get install -y \
    curl \
    git \
    nano \
    build-essential \
    cmake \
    sudo \
    gosu \
    wget \
    unzip \
	screen
	
###################################
# Setup Anaconda
###################################
# last cuda version, to change - LASTEST_CONDA
ARG LATEST_CONDA="latest"
ENV LATEST_CONDA=$LATEST_CONDA
ENV CONDA_HOME="/opt/anaconda3"

# download and install conda
# RUN curl --silent -O https://repo.continuum.io/archive/Anaconda3-$LATEST_CONDA-Linux-x86_64.sh \
#     && bash Anaconda3-$LATEST_CONDA-Linux-x86_64.sh -b -p ${CONDA_HOME}
RUN curl --silent -O https://repo.anaconda.com/miniconda/Miniconda3-$LATEST_CONDA-Linux-x86_64.sh \
    && bash Miniconda3-$LATEST_CONDA-Linux-x86_64.sh -b -p ${CONDA_HOME}
RUN rm Miniconda3-$LATEST_CONDA-Linux-x86_64.sh

# setup environment variable for anaconda
ENV CONDA_PATH="${CONDA_HOME}/bin"
ENV CONDA_LIB="${CONDA_HOME}/lib"

ENV JUPYTER_CONFIG_DIR="${CONDA_HOME}/.jupyter/config"
ENV JUPYTER_DATA_DIR="${CONDA_HOME}/.jupyter/data"
ENV CONDARC="${CONDA_HOME}/.condarc"
ENV CONDA_PKGS_DIRS="${CONDA_HOME}/.conda/pkgs"
ENV CONDA_ENVS_PATH="${CONDA_HOME}/.conda/envs"
ENV IPYTHONDIR="${CONDA_HOME}/.ipython"

ENV PATH="${CONDA_PATH}:${PATH}"
ENV LD_LIBRARY_PATH="${CONDA_LIB}:${LD_LIBRARY_PATH}"

###################################
# Setup Anaconda Environment Base
# + Jupyter-Lab, and Plugins
###################################
RUN conda update -n base -c defaults conda
RUN python -m pip install --upgrade pip
RUN conda install -y -n base -c anaconda jupyter jupyterlab nodejs widgetsnbextension

RUN . activate base
RUN pip install jupyterlab==1.0.1 # solve error sidebar
RUN jupyter nbextension enable --py widgetsnbextension
RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager
RUN jupyter labextension install @jupyterlab/toc
RUN jupyter lab clean
RUN jupyter lab build
RUN . deactivate

###################################
# Init Working Directory
###################################
# Construct workspace
ARG HOME_DIR="/ws"
ENV HOME_DIR=$HOME_DIR
RUN mkdir -p ${HOME_DIR}/config

###################################
# Setup Anaconda Environment: Cur37
###################################
# create environment from file
ARG CONDA_ENV_01="cur37"   
ENV CONDA_ENV_01=$CONDA_ENV_01
COPY ${CONDA_ENV_01}.yml ${HOME_DIR}/config/
RUN conda env create -n ${CONDA_ENV_01} -f ${HOME_DIR}/config/${CONDA_ENV_01}.yml

# update environment
RUN . activate ${CONDA_ENV_01}
RUN python -m ipykernel install --user --name ${CONDA_ENV_01} --display-name "${CONDA_ENV_01}"
# Fix CafeGpu
RUN conda install -y -c defaults protobuf libprotobuf glog leveldb
RUN . deactivate

###################################
# Finish Setup
###################################
RUN mkdir -p ${HOME_DIR}/bin \
    && mkdir -p ${HOME_DIR}/projects \
    && mkdir -p ${HOME_DIR}/media \
    && mkdir -p ${HOME_DIR}/logs

WORKDIR ${HOME_DIR}
ENTRYPOINT ["jupyter", "lab","--ip=0.0.0.0", "--allow-root"]
CMD [""--port=8080"]
EXPOSE 8080
