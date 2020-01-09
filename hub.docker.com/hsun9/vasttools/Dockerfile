FROM ubuntu:xenial

#some basic tools
RUN apt-get update -y && apt-get install -y --no-install-recommends \
    build-essential \
    bzip2 \
    curl \
    csh \
    default-jdk \
    default-jre \
    emacs \
    emacs-goodies-el \
    ess \
    evince \
    g++ \
    gawk \
    git \
    grep \
    less \
    libcurl4-openssl-dev \
    libpng-dev \
    librsvg2-bin \
    libssl-dev \
    libxml2-dev \
    lsof \
    make \
    man \
    ncurses-dev \
    nodejs \
    openssh-client \
    pdftk \
    pkg-config \
    python \
    rsync \
    screen \
    tabix \
    unzip \
    wget \
    zip \
    zlib1g-dev


# install vast-tools
RUN mkdir /opt/vastTools && \
    cd /opt/vastTools && \
    git clone https://github.com/vastgroup/vast-tools.git . && \
    ln -s /opt/vastTools/vast-tools /usr/bin/vast-tools


# miniconda archive
# https://repo.continuum.io/miniconda/
RUN echo "export PATH=/opt/conda/bin:$PATH" > /etc/profile.d/conda.sh && \
    curl -L https://repo.continuum.io/miniconda/Miniconda3-4.3.31-Linux-x86_64.sh -o ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

ENV PATH /opt/conda/bin:$PATH

# bowtie1
RUN conda install -c bioconda bowtie=1.2.2
RUN conda install -c bioconda coreutils

# R-packages
RUN conda config --add channels conda-forge 
RUN conda install r-optparse r-reshape2 r-rcolorbrewer r-ggplot2 r-mass r-devtools  

# independent R-package psiplot
RUN ln -s /bin/tar /bin/gtar
RUN R -e 'devtools::install_github("kcha/psiplot")'


WORKDIR /usr/local/work

CMD ["vast-tools"]
