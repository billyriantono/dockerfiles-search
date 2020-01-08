# A mash up of the following Dockerfiles:
# https://github.com/GenomicParisCentre/dockerfiles/blob/master/deepbinner/0.2.0/Dockerfile
# https://github.com/ContinuumIO/docker-images/blob/master/miniconda3/debian/Dockerfile

FROM ubuntu:18.04

# Set non-interactive mode
# ENV DEBIAN_FRONTEND noninteractive
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# Install Deepbinner and its dependencies
RUN apt-get update --fix-missing && \
    apt-get install -y \
        git \
        build-essential \
        python3.7 \
        python3-pkg-resources \
        python3-pip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV TINI_VERSION v0.16.1
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini

# use forked repo and specify commit
RUN pip3 install git+git://github.com/rrwick/Deepbinner.git@319bae84bfb3b0f3ab279b70e9e0a886156414bf

RUN echo "hola mundo"




