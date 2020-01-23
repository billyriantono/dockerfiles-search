FROM ubuntu:bionic-20190204

################## METADATA ######################
LABEL base.image="ubuntu:bionic-20190204"
LABEL version="0.1"
LABEL software="seekr"
LABEL software.version="c624cf4ba9455ae97055f56709f8e983230e1bfc"
LABEL about.summary="image for seekr: Find communities of nucleotide sequences based on kmer frequencies"
LABEL about.tags="Bioinformatics, kmer analysis, transcripts"

################## MAINTAINER ######################
MAINTAINER Youhuang Bai <youhuang.bai.1@vumc.org>

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y python3 \
        python3-pip \
        software-properties-common \
        build-essential \
        unzip \
        cmake \
        make \
        autoconf \
        automake \
        libtool \
        libtool-bin \
        gettext \
        git \
        vim \
        wget \
        locales \
        dialog \
        apt-utils \
        parallel \
        libxml2-dev \
        zlib1g-dev \
        python-igraph \
        gfortran && \
    apt-get clean && \
    apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/*

RUN pip3 install seekr



