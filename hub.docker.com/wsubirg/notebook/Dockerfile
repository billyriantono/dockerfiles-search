# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.

# Ubuntu 16.04 (xenial) from 2017-07-23
# https://github.com/docker-library/official-images/commit/0ea9b38b835ffb656c497783321632ec7f87b60c
#FROM ubuntu@sha256:84c334414e2bfdcae99509a6add166bbb4fa4041dc3fa6af08046a66fed3005f
FROM nvidia/cuda:9.0-devel-ubuntu17.04
LABEL maintainer="Daniel P. Foose <dpfoose@gmail.com>"

# Install all OS dependencies for notebook server that starts but lacks all
# features (e.g., download as all possible file formats)
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get -yq dist-upgrade \
 && apt-get install -yq --no-install-recommends \
    libopenblas-dev \
    wget \
    bzip2 \
    ca-certificates \
    sudo \
    locales \
    fonts-liberation \
    build-essential \
    emacs \
    git \
    inkscape \
    jed \
    libsm6 \
    libxext-dev \
    libxrender1 \
    lmodern \
    pandoc \
    python-dev \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    texlive-generic-recommended \
    texlive-latex-base \
    texlive-latex-extra \
    texlive-xetex \
    vim \
    unzip \
    fonts-dejavu \
    tzdata \
    gfortran 
    
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen

# Install Tini
RUN wget --quiet https://github.com/krallin/tini/releases/download/v0.10.0/tini && \
    echo "1361527f39190a7338a0b434bd8c88ff7233ce7b9a4876f3315c22fce7eca1b0 *tini" | sha256sum -c - && \
    mv tini /usr/local/bin/tini && \
    chmod +x /usr/local/bin/tini

# Configure environment
ENV CONDA_DIR=/opt/conda \
    SHELL=/bin/bash \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8
ENV PATH=$CONDA_DIR/bin:$PATH \
    HOME=/home/$NB_USER

ADD fix-permissions /usr/local/bin/fix-permissions
# Create jovyan user with UID=1000 and in the 'users' group
# and make sure these dirs are writable by the `users` group.
RUN mkdir -p $CONDA_DIR
#RUN fix-permissions $HOME && \
#    fix-permissions $CONDA_DIR


# install miniconda
RUN cd /tmp && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    /bin/bash Miniconda3-latest-Linux-x86_64.sh -f -b -p$CONDA_DIR && \
    rm Miniconda3-latest-Linux-x86_64.sh && \
    $CONDA_DIR/bin/conda config --system --prepend channels conda-forge && \
    $CONDA_DIR/bin/conda config --system --set auto_update_conda false && \
    $CONDA_DIR/bin/conda config --system --set show_channel_urls true && \
    $CONDA_DIR/bin/conda update --all --quiet --yes && \
    $CONDA_DIR/bin/conda clean -tipsy 

# set up miniconda python envs
ADD environment3.yml /tmp/
ADD environment2.yml /tmp/
RUN $CONDA_DIR/bin/conda install notebook jupyterlab widgetsnbextension jupyterhub
RUN $CONDA_DIR/bin/conda env create -f /tmp/environment3.yml
RUN $CONDA_DIR/bin/conda env create -f /tmp/environment2.yml

#install non-env dependencies (what is used to launch the notebook server):
RUN $CONDA_DIR/bin/conda clean -tipsy
RUN jupyter labextension install @jupyterlab/hub-extension && \
    rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
    jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager

#remove qt packages installed with matplot lib to reduce image size
RUN /bin/bash -c "source $CONDA_DIR/bin/activate py27 && \
    conda remove --quiet --yes --force qt pyqt"
RUN /bin/bash -c "source $CONDA_DIR/bin/activate py36 && \
    conda remove --quiet --yes --force qt pyqt"

# Install facets which does not have a pip or conda package at the moment
RUN cd /tmp && \
    git clone https://github.com/PAIR-code/facets.git && \
    cd facets && \
    jupyter nbextension install facets-dist/ --sys-prefix && \
    rm -rf facets

#install the 3.6 and 2.7 kernels
RUN /bin/bash -c "source $CONDA_DIR/bin/activate py36 && ipython kernel install --name py36"
RUN /bin/bash -c "source $CONDA_DIR/bin/activate py27 && ipython kernel install --name python-2.7"

# Julia dependencies
# install Julia packages in /opt/julia instead of $HOME
ENV JULIA_PKGDIR=/opt/julia
ENV JULIA_VERSION=0.6.1
RUN mkdir /opt/julia-0.6.1 && \
    cd /tmp && \
    wget https://julialang-s3.julialang.org/bin/linux/x64/0.6/julia-0.6.1-linux-x86_64.tar.gz && \
    tar xzf julia-0.6.1-linux-x86_64.tar.gz -C /opt/julia-0.6.1 --strip-components=1 && \
    rm /tmp/julia-0.6.1-linux-x86_64.tar.gz
RUN ln -fs /opt/julia-*/bin/julia /usr/local/bin/julia

# Show Julia where conda libraries are \
RUN mkdir /etc/julia && \
    echo "push!(Libdl.DL_LOAD_PATH, \"$CONDA_DIR/lib\")" >> /etc/julia/juliarc.jl && \
    echo "" >> /etc/julia/juliarc.jl && \
    echo "push!(Libdl.DL_LOAD_PATH, \"$CONDA_DIR/envs/py36/lib\")" >> /etc/julia/juliarc.jl && \
    mkdir $JULIA_PKGDIR
# Add Julia packages
# to the system share location. Avoids problems with runtime UID change not
# taking effect properly on the .local folder in the birg home dir.
RUN julia -e 'Pkg.init()' && \
    julia -e 'Pkg.update()' && \
    julia -e 'Pkg.add("HDF5")' && \
    julia -e 'Pkg.add("Gadfly")' && \
    julia -e 'Pkg.add("RDatasets")' && \
    julia -e 'Pkg.add("IJulia")' && \
    # Precompile Julia packages \
    julia -e 'using HDF5' && \
    julia -e 'using Gadfly' && \
    julia -e 'using RDatasets' && \
    julia -e 'using IJulia' && \
    # move kernelspec out of home \
    mv $HOME/.local/share/jupyter/kernels/julia* $CONDA_DIR/envs/py36/share/jupyter/kernels/ && \
    chmod -R go+rx $CONDA_DIR/share/jupyter && \
    rm -rf $HOME/.local

EXPOSE 8888
WORKDIR $HOME

# Configure container startup
ENTRYPOINT ["tini", "--"]
CMD ["start-singleuser.sh"]

# Add local files as late as possible to avoid cache busting
COPY start.sh /usr/local/bin/
COPY start-notebook.sh /usr/local/bin/
COPY start-singleuser.sh /usr/local/bin/
COPY jupyter_notebook_config.py /etc/jupyter/

# Import matplotlib the first time to build the font cache.
ENV XDG_CACHE_HOME /home/$NB_USER/.cache/
RUN /bin/bash -c "source $CONDA_DIR/bin/activate py36 && \
    MPLBACKEND=Agg python -c \"import matplotlib.pyplot\""
RUN /bin/bash -c "source $CONDA_DIR/bin/activate py27 && \
    MPLBACKEND=Agg python -c \"import matplotlib.pyplot\""

ADD nvblas.conf /usr/local/cuda
ENV NVBLAS_CONFIG_FILE=/usr/local/cuda/nvblas.conf
RUN echo "NVBLAS_CONFIG_FILE=/usr/local/cuda/nvblas.conf" >> /etc/profile.d/nvblas.sh
#RUN echo "/usr/local/cuda/lib64/libnvblas.so /usr/lib/libopenblas.so" >> /etc/ld.so.preload
# Switch back to birg to avoid accidental container runs as root
ENV LD_PRELOAD /usr/local/cuda/lib64/libnvblas.so /usr/lib/libopenblas.so
