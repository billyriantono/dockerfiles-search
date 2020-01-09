FROM ubuntu:xenial
MAINTAINER John Garza <johnegarza@wustl.edu>

LABEL \
    description="Image containing pyyaml for use in utility scripts"

RUN apt-get update && apt-get install -y \
    python-pip

RUN pip install --upgrade pip
RUN pip install pyyaml

COPY staging.py /usr/bin/staging.py
