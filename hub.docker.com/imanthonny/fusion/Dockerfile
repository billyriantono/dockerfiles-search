FROM ubuntu:16.04

RUN apt-get -y clean \
    && apt-get -y update \
    && apt-get -y install \
    wget \
    gawk \
    gcc \ 
    g++ \
    make \ 
    cmake \ 
    automake \
    curl \ 
    unzip \ 
    zip \
    bzip2 \
    tar \
    gzip \
    pigz \
    parallel \
    build-essential \
    libncurses5-dev \
    libc6-dev \
    zlib1g \
    zlib1g-dev \
    libtbb-dev \
    libtbb2 \
    python \
    python-dev \
    python-numpy \
    python-biopython \
    python-xlrd \
    python-openpyxl \
    default-jdk

######################
## INSTALLATION
######################

RUN wget http://sf.net/projects/fusioncatcher/files/bootstrap.py -O bootstrap.py \
    && yes Y | python bootstrap.py
    
    

