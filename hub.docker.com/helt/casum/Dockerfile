FROM python:2.7-wheezy

# File Author / Maintainer
MAINTAINER Hendrik Luecketieke <opensource@luecke-tieke.de>

USER root
RUN apt-get update && apt-get install -y --no-install-recommends \
        glpk \
        libxml-dom-perl \
        && rm -rf /var/lib/apt/lists/*
