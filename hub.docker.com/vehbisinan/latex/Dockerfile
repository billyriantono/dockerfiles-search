FROM ubuntu:16.10

## Defines the version of the LaTeX Docker image:
ENV DOCKER_LATEX_VERSION=1

## Configure package system, install LaTeX + other required packages, and finally cleanup:
RUN echo "debconf debconf/frontend select Noninteractive" | debconf-set-selections && \
    apt-get update -qy && \
    apt-get install -qy texlive-full biber latexmk make nano vim unzip && \
    apt-get clean autoclean && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
