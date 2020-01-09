##### BASE IMAGE #####
FROM debian:9.3

##### METADATA #####
LABEL base.image="debian:9.3"
LABEL version="1"
LABEL software="stringtie"
LABEL software.version="1.3.5"
LABEL software.description="StringTie is a fast and highly efficient assembler of RNA-Seq alignments"
LABEL software.website="https://ccb.jhu.edu/software/stringtie/"
LABEL software.documentation="https://ccb.jhu.edu/software/stringtie/"
LABEL software.license="https://ccb.jhu.edu/software/stringtie/#contact"
LABEL software.tags="Genomics, Transcriptomics"
LABEL maintainer="foivos.gypas@unibas.ch"
LABEL maintainer.organisation="Biozentrum, University of Basel"
LABEL maintainer.location="Klingelbergstrasse 50/70, CH-4056 Basel, Switzerland"
LABEL maintainer.lab="Zavolan Lab"
LABEL maintainer.license="https://spdx.org/licenses/Apache-2.0"

##### INSTALL #####
RUN apt-get update -y \
  && apt-get install -y wget make gcc build-essential zlib1g-dev libncurses5-dev samtools msmtp zlib1g-dev make libncurses5-dev libxml2-dev \
  && wget http://ccb.jhu.edu/software/stringtie/dl/stringtie-1.3.5.Linux_x86_64.tar.gz \
  && tar xzvf stringtie-1.3.5.Linux_x86_64.tar.gz \
  && cp stringtie-1.3.5*/stringtie /usr/local/bin \
  && rm -rf stringtie-1.3.5.Linux_x86_64.tar.gz \
  && apt-get purge -y wget \
  && apt-get autoremove -y && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
