FROM ubuntu:14.04

MAINTAINER Thiago Falcao "thiagofalcao@gmail.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get upgrade -y && apt-get install -y \
    build-essential \
    ca-certificates \
    gcc \
    git \
    libpq-dev \
    make \
    python2.7 \
    python2.7-dev \
    python-pip \
    python-mock \
    python-nose \
    python-coverage \
    pylint \
    ssh \
    && apt-get autoremove \
    && apt-get clean


RUN pip install -U setuptools
RUN pip install -U virtualenv
RUN pip install -U mock
RUN pip install -U nose
RUN pip install -U coverage
RUN pip install -U pylint
