FROM ubuntu:16.04
MAINTAINER Cristian Balas

# Install apt packages
RUN apt-get update && apt-get -y upgrade && apt-get -y dist-upgrade && apt-get install -y \
    aptitude \
    curl \
    wget \
    htop \
    iotop \
    libffi-dev \
    libssl-dev \
    liblzma-dev \
    python \
    python-pip \
    python-dev \
    screen \
    supervisor \
    vim

RUN pip install -U \
    pip \
    virtualenv \
    pipenv \
    pymongo \
    python-dateutil \
    ipython==5.3 \
    httpie \
    requests[security]

COPY vimrc /root/.vimrc

RUN mkdir /app
WORKDIR /app


CMD /bin/bash
