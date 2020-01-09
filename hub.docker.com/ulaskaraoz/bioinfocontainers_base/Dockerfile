# Set the base image
FROM ubuntu:16.04

MAINTAINER Ulas Karaoz <ukaraoz@lbl.gov>

################## METADATA ######################

LABEL base_image="ubuntu:16.04"
LABEL version="4"
LABEL software="BioinfoContainers base Image"
LABEL software.version="1.0.0"
LABEL about.summary="Base image for BioinfoContainers"
#LABEL about.home="http://biocontainers.pro"
#LABEL about.documentation="https://github.com/BioContainers/specs/wiki"
#LABEL about.license_file="https://github.com/BioContainers/containers/blob/master/LICENSE"
#LABEL about.license="SPDX:Apache-2.0"
#LABEL about.tags="Genomics,Proteomics,Transcriptomics,General,Metabolomics"

# Set environmental variable
ENV DEBIAN_FRONTEND noninteractive

# update package sources
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bkp && \
    bash -c 'echo -e "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial main restricted universe multiverse\n\
deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-updates main restricted universe multiverse\n\
deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-backports main restricted universe multiverse\n\
deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-security main restricted universe multiverse\n\n" > /etc/apt/sources.list' && \
    cat /etc/apt/sources.list.bkp >> /etc/apt/sources.list && \
    cat /etc/apt/sources.list

# install -y assumes 'yes' to all commands
RUN apt-get clean all && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y  \
        autotools-dev   \
        automake        \
        cmake           \
        curl            \
        grep            \
        sed             \
        dpkg            \
        fuse            \
        git             \
        wget            \
        zip             \
        openjdk-8-jre   \
        build-essential \
        pkg-config      \
        python          \
	    python-dev      \
        python-pip      \
        bzip2           \
        ca-certificates \
        libglib2.0-0    \
        libxext6        \
        libsm6          \
        libxrender1     \
        git             \
        zlib1g-dev &&   \
        apt-get clean && \
        apt-get purge && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install miniconda in batch mode (-b) and under /opt/conda (-p)
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda2-4.0.5-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

# Tini - A tiny but valid init for containers
# 
RUN TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` && \
    curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb && \
    dpkg -i tini.deb && \
    rm tini.deb && \
    apt-get clean

RUN mkdir /data /config


# Without any other option provided, processes in containers will execute as root 
# (unless a different uid was supplied in the Dockerfile)
# user
# Add user appuser with password appuser
RUN groupadd fuse && \
    useradd --create-home --shell /bin/bash --user-group --uid 1000 --groups sudo,fuse appuser && \
    echo `echo "appuser\appuser\n" | passwd appuser` && \
    chown appuser:appuser /data && \
    chown appuser:appuser /config

# give write permissions to conda folder
RUN chmod 777 -R /opt/conda/

# Change user
USER appuser

ENV PATH=$PATH:/opt/conda/bin
ENV PATH=$PATH:/home/appuser/bin
ENV HOME=/home/appuser

RUN mkdir /home/appuser/bin

RUN conda config --add channels r
RUN conda config --add channels bioconda

RUN conda upgrade conda

VOLUME ["/data", "/config"]

# Overwrite this with 'CMD []' in a dependent Dockerfile
CMD ["/bin/bash"]

WORKDIR /data