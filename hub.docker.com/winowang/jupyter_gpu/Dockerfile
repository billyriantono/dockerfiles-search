# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.

#https://hub.docker.com/r/nvidia/cuda/tags/

#FROM nvidia/cuda:9.0-base-ubuntu16.04
FROM nvidia/cuda:9.2-cudnn7-runtime-ubuntu18.04
#FROM nvidia/cuda:10.0-cudnn7-runtime-ubuntu18.04
#FROM nvidia/cuda:9.2-cudnn7-devel-ubuntu18.04

LABEL maintainer="Jupyter Scipybase"

ENV CUDNN_VERSION=7.5.0.56-1+cuda9.2
ENV NCCL_VERSION=2.4.7-1+cuda9.2

#USER root

# Install all OS dependencies for notebook server that starts but lacks all
# features (e.g., download as all possible file formats)
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get -yq dist-upgrade \
 && apt-get install -yq --no-install-recommends --allow-change-held-packages \
    build-essential \
    curl \
    libfreetype6-dev \
    libhdf5-serial-dev \
    libpng-dev \
    libzmq3-dev \
    #libcudnn7=${CUDNN_VERSION} \
    libnccl2=${NCCL_VERSION} \
    libnccl-dev=${NCCL_VERSION} \
    iputils-ping \
    net-tools \
    dh-autoreconf \
    wget \
    bzip2 \
    ca-certificates \
    sudo \
    locales \
    fonts-liberation \
    libncurses5-dev \
    vim \
    git \
    jed \
    libsm6 \
    libxext-dev \
    libxrender1 \
    lmodern \
    netcat \
    pandoc \
    python-dev \
    unzip \
    nano \
    openssh-server \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen

# Install Tini
RUN wget --quiet https://github.com/krallin/tini/releases/download/v0.18.0/tini && \
    echo "12d20136605531b09a2c2dac02ccee85e1b874eb322ef6baf7561cd93f93c855 *tini" | sha256sum -c - && \
    mv tini /usr/local/bin/tini && \
    chmod +x /usr/local/bin/tini

# Configure environment
ENV CONDA_DIR=/opt/conda \
    SHELL=/bin/bash \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8
#ENV PATH=$CONDA_DIR/bin:$PATH \
ENV PATH=$CONDA_DIR/bin:$PATH
   # HOME=/home

#USER root
RUN mkdir -p $CONDA_DIR && \ 
# Setup work directory for backward-compatibility
    mkdir /home/work 

# Install conda and check the md5 sum provided on the download site
ENV MINICONDA_VERSION 4.5.4
RUN cd /tmp && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-${MINICONDA_VERSION}-Linux-x86_64.sh && \
    echo "a946ea1d0c4a642ddf0c3a26a18bb16d *Miniconda3-${MINICONDA_VERSION}-Linux-x86_64.sh" | md5sum -c - && \
    /bin/bash Miniconda3-${MINICONDA_VERSION}-Linux-x86_64.sh -f -b -p $CONDA_DIR && \
    rm Miniconda3-${MINICONDA_VERSION}-Linux-x86_64.sh && \
    $CONDA_DIR/bin/conda config --system --prepend channels conda-forge && \
    $CONDA_DIR/bin/conda config --system --set auto_update_conda false && \
    $CONDA_DIR/bin/conda config --system --set show_channel_urls true && \
    $CONDA_DIR/bin/conda install --quiet --yes conda="${MINICONDA_VERSION%.*}.*" && \
    $CONDA_DIR/bin/conda update --all --quiet --yes && \
    conda clean -tipsy && \
    rm -rf /home/.cache/yarn 

# Install Jupyter Notebook and Hub
#RUN conda install --quiet --yes \
RUN conda install --yes \
    'notebook=5.7.*' && \
    conda clean -tipsy && \
    #npm cache clean --force && \
    #rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
    rm -rf /home/.cache/yarn 

#USER root
#EXPOSE 8888
WORKDIR $HOME/work

# Configure container startup
#ENTRYPOINT ["tini", "-g", "--"]
#CMD ["start-notebook.sh"]

# Add local files as late as possible to avoid cache busting
RUN wget -P /usr/local/bin/  https://raw.githubusercontent.com/jupyter/docker-stacks/master/base-notebook/start.sh && \
    wget -P /usr/local/bin/  https://raw.githubusercontent.com/jupyter/docker-stacks/master/base-notebook/start-notebook.sh && \
    wget -P /usr/local/bin/  https://raw.githubusercontent.com/jupyter/docker-stacks/master/base-notebook/start-singleuser.sh && \
    wget -P /etc/jupyter/    https://raw.githubusercontent.com/jupyter/docker-stacks/master/base-notebook/jupyter_notebook_config.py

# ffmpeg for matplotlib anim
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg && \
    apt-get install -y --no-install-recommends libssl-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

#RUN conda install --quiet --yes \
RUN conda install --yes \
    'conda-forge::blas=*=openblas' \
    'ipywidgets=7.2*' \
    'pandas=0.23*' \
   # 'numexpr=2.6*' \
    'matplotlib=3.0*' \
    'numpy=1.15*' \
    'scipy=1.1*' \
    'opencv=3.4*' \
   # 'seaborn=0.8*' \
   # 'sympy=1.1*' \
   # 'cython=0.28*' \
   # 'patsy=0.5*' \
   # 'statsmodels=0.9*' \
   # 'dill=0.2*' \
    'numba=0.38*' \
   # 'bokeh=0.12*' \
   # 'sqlalchemy=1.2*' \
   # 'hdf5=1.10*' \
   # 'h5py=2.7*' \
   # 'xlrd'  && \
    'pillow=5.3*' &&\
   # conda remove --quiet --yes --force qt pyqt && \
    conda clean -tipsy && \
    
    conda update --yes  -n base conda && \
    
    #npm cache clean --force && \
    rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
    rm -rf /home/.cache/yarn && \
    rm -rf /home/.node-gyp 
    
RUN echo export PATH="/opt/conda/bin:$PATH" >> /root/.bashrc 
RUN echo PermitRootLogin yes >> /etc/ssh/sshd_config 
#RUN echo "root:111111" | chpasswd

CMD ["sudo /etc/init.d/ssh start"]
