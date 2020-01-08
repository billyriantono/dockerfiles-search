FROM ubuntu

# Define working directory.
RUN mkdir -p /apps
RUN mkdir -p /data
WORKDIR /apps  

# Install requirements
RUN apt-get update && \
  apt-get -y install \
  wget \
  python \
  unzip \
  git \
  htop \
  python-qt4 \
  alien \
  python-tk \
  vim \
  aria2 \
  python-pip \
  python-dev \
  build-essential \
  liblzma-dev \
  zlib1g-dev \
  libncurses5-dev \
  libbz2-1.0 libbz2-dev libbz2-ocaml libbz2-ocaml-dev \
  gcc \
  make \
  libncurses-dev \
  autoconf \
  libdb-dev 

WORKDIR /data
