# Distributed under the terms of the Modified BSD License.
FROM jupyter/base-notebook

USER root

# General system packages
RUN apt-get update && apt-get install -yq --no-install-recommends \
    python3-software-properties \
    software-properties-common \
    apt-utils \
    gnupg2 \
    fonts-dejavu \
    tzdata \
    gfortran \
    curl \
    less \
    gcc \
    g++ \
    clang-6.0 \
    openssh-client \
    openssh-server \
    cmake \
    python-dev \
    libgsl-dev \
    libssl-dev \
    libcurl4-openssl-dev \
    libxml2 \
    libxml2-dev \
    libapparmor1 \
    libedit2 \
    libhdf5-dev \
    libclang-dev \
    lsb-release \
    psmisc \
    rsync \
    vim \
    default-jdk \
    libbz2-dev \
    libpcre3-dev \
    liblzma-dev \
    zlib1g-dev \
    xz-utils \
    liblapack-dev \
    libopenblas-dev \
    libigraph0-dev \
    libreadline-dev \
    libblas-dev \
    libtiff5-dev \
    fftw3-dev \
    git \
    hdf5-tools \
    libffi-dev \
    gettext \
    texlive-xetex \
    libpng-dev \
    libpixman-1-0 \ 
    fuse libfuse2 sshfs \
    libxkbcommon-x11-0 \
    openjdk-8-jdk \
    wget \
    gdal-bin \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install R
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
RUN add-apt-repository ppa:marutter/c2d4u3.5
RUN echo "deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/" | sudo tee -a /etc/apt/sources.list
RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
    littler r-cran-littler r-base r-base-dev r-recommended &&\
	rm -rf /tmp/downloaded_packages/ /tmp/*.rds && \
	rm -rf /var/lib/apt/lists/*

# R packages
RUN Rscript -e 'install.packages(c("devtools", "BiocManager"), dependencies = TRUE)'

# Add usert jovyan to the staff group
RUN usermod -a -G staff ${NB_USER}

# Set R libs path outside jovyan profile
ENV R_LIBS_USER=/usr/local/lib/R/site-library

# Install Bioconductor
RUN Rscript -e 'BiocManager::install()'

# Python packages
RUN pip install scipy scanpy python-igraph louvain bbknn rpy2 leidenalg pandas

# Conda packages
RUN conda install --quiet --yes nb_conda_kernels conda-build

# Fix permissions
RUN conda build purge-all && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

# RStudio Server (1.2.5019)
ENV RSTUDIO_PKG=rstudio-server-1.2.5019-amd64.deb
RUN wget -q -O /tmp/rstudio.deb https://download2.rstudio.org/server/bionic/amd64/${RSTUDIO_PKG}
RUN apt-get update && \
    apt-get install -y /tmp/rstudio.deb && \
    rm /tmp/rstudio.deb && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
ENV PATH=$PATH:/usr/lib/rstudio-server/bin

# Shiny Server (1.5.9.923)
ENV SHINY_PKG=shiny-server-1.5.9.923-amd64.deb
RUN wget -q -O /tmp/shiny-server.deb https://download3.rstudio.org/ubuntu-14.04/x86_64/${SHINY_PKG}
RUN apt-get update && \
    apt-get install -y /tmp/shiny-server.deb && \
    rm /tmp/shiny-server.deb && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# jupyter-rsession-proxy (latest)
RUN python3 -m pip install jupyter-server-proxy jupyter-rsession-proxy
RUN jupyter labextension install @jupyterlab/server-proxy

# Give user jovyan sudo permissions
RUN sed -i -e "s/Defaults    requiretty.*/ #Defaults    requiretty/g" /etc/sudoers
RUN echo "${NB_USER} ALL= (ALL) NOPASSWD: ALL" >> /etc/sudoers.d/${NB_USER}