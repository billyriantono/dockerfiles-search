FROM centos:7.6.1810

MAINTAINER Hassan Foroughi hassan.foroughi@scilifelab.se 

LABEL Description="This image is used to run FusionCatcher" Version="1.20"

RUN yum install -y epel-release \
    && yum install -y \
    automake \
    which \
    git \
    bzip2 \
    cmake \
    curl \
    gawk \
    gcc \
    gzip  \
    ncurses \
    ncurses-devel \
    make \
    pigz \
    tar \
    unzip \
    wget \
    zlib-devel \
    java-1.8.0-openjdk* \
    tbb-devel \
    glibc-devel \
    python-devel \
    numpy \
    python-biopython \
    && wget --no-check-certificate http://sf.net/projects/fusioncatcher/files/bootstrap.py -O bootstrap.py \
    && python bootstrap.py --help \
    && python bootstrap.py -t -y -i /opt/fusioncatcher/v1.20/

WORKDIR /opt
