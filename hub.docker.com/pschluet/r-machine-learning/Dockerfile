FROM ubuntu:18.04

LABEL maintainer="Paul Schlueter <paul@paulschlueter.com>"

ENV DEBIAN_FRONTEND=noninteractive 

# Add CRAN repository to enable R 3.6
RUN apt-get -y update && apt-get install -y --install-recommends \
    apt-transport-https \
    software-properties-common \
    dirmngr \
    gpg-agent && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9 && \
    add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/'

RUN apt-get -y update && apt-get install -y --no-install-recommends \
    wget \
    r-base=3.6.1-3bionic \
    r-base-dev=3.6.1-3bionic \
    libcurl4-openssl-dev \
    libxml2-dev \
    libssl-dev \
    ca-certificates

# Add the Python requests library for integration tests
RUN apt-get -y install python3-pip && \
    pip3 install requests==2.22.0

COPY install-packages.R install-packages.R
RUN Rscript install-packages.R
