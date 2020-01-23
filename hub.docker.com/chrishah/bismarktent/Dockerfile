#FROM rocker/r-ver:3.5.1
FROM bioconductor/release_core2:R3.5.2_Bioc3.8
MAINTAINER c.a.miller@wustl.edu
LABEL Image for ad-hoc bisulfite seq processing in R

#add a few useful tools
RUN apt-get update -y && apt-get install -y --no-install-recommends \
    curl \
    emacs \
    emacs-goodies-el \
    ess \
    wget \
    pdftk \
    rsync \
    libxml2-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libbz2-dev \
    liblzma-dev \
    libpng-dev \
    bzip2

#add r packages
ADD rpackages.R /tmp/
RUN R -f /tmp/rpackages.R
