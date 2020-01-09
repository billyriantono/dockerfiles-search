FROM ubuntu:trusty

MAINTAINER github.com/jtdoepke

ENV TOX_VERSION 2.7.0
ENV PYTHON_VERSIONS "2.6 2.7 3.2 3.3 3.4 3.5 3.6"

COPY install-pythons.sh /
RUN /install-pythons.sh

RUN apt-get update && apt-get install -y python-pip && rm -rf /var/lib/apt/lists/*
RUN pip install "tox==${TOX_VERSION}"
