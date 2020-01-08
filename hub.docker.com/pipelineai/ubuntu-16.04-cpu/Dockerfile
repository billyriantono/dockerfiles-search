FROM ubuntu:xenial-20180123

ENV \
  OS_LOCALE="C.UTF-8"

ENV \
  LANG=$OS_LOCALE \
  LANGUAGE=en_US:en \
  LC_ALL=$OS_LOCALE

ENV \
  DEBIAN_FRONTEND noninteractive

ENV \
  TERM=xterm

RUN \
  echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

ENV \
  SHELL=/bin/bash

RUN \
  rm /bin/sh \
  && ln -s /bin/bash /bin/sh

RUN \
 apt-get update \
 && apt-get install -y --no-install-recommends \
        apt-utils \
        apt-transport-https \
        build-essential \
        software-properties-common \
        python-software-properties \ 
        daemontools \
        curl \
        wget \
        vim \
        git \
        zip \
        bzip2 \
        libcurl3-dev \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
        python-dev \
        python3-dev \
        python-numpy \
        python3-numpy \ 
        python-six \
        python3-six \
        python-wheel \
        python3-wheel \
        python-pip \ 
        python3-pip \
        rsync \
        software-properties-common \
        swig \ 
        unzip \
        zip \
        zlib1g-dev \
        locales \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN \
  locale-gen en_US.UTF-8 \
  && localedef -i en_US -f UTF-8 en_us.UTF-8

RUN wget -q https://repo.continuum.io/miniconda/Miniconda3-4.3.31-Linux-x86_64.sh -O /tmp/miniconda.sh  && \
    echo '7fe70b214bee1143e3e3f0467b71453c */tmp/miniconda.sh' | md5sum -c - && \
    bash /tmp/miniconda.sh -f -b -p /opt/conda && \
    /opt/conda/bin/conda install --yes python=3.6 pip && \
    /opt/conda/bin/pip install --upgrade pip && \
    rm /tmp/miniconda.sh

# Update normal pip
RUN \
  pip install -U --no-cache --ignore-installed pip

ENV \
  PATH=/opt/conda/bin:$PATH

###################
# Setup OpenJDK 1.8
###################
RUN \
  apt-get update \
  && apt-get install -y software-properties-common \
  && add-apt-repository -y ppa:openjdk-r/ppa \
  && apt-get update \
  && apt-get install -y --no-install-recommends openjdk-8-jdk openjdk-8-jre-headless \
  && apt-get install -y apt-transport-https \
  && apt-get install -y wget \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

ENV \
  JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/

COPY sysutils/container-limits.sh sysutils/container-limits.sh
