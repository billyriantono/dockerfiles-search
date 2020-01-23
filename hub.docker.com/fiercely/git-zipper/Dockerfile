##### BASE IMAGE #####
FROM python:3.6.5

##### METADATA #####
LABEL base.image="python:3.6.5"
LABEL version="1"
LABEL software="Python and pysam"
LABEL software.version="3.6.5_0.15.1"
LABEL software.description="Python programming language|python module for reading, manipulating and writing genomic data sets"
LABEL software.website="https://www.python.org/|https://pysam.readthedocs.io/en/stable/"
LABEL software.documentation="https://docs.python.org/3/|https://pysam.readthedocs.io/en/stable/"
LABEL software.license="https://docs.python.org/3/license.html|"
LABEL software.tags="General|Genomics,Transcriptomics"
LABEL maintainer="foivos.gypas@unibas.ch"
LABEL maintainer.organisation="Biozentrum, University of Basel"
LABEL maintainer.location="Klingelbergstrasse 50/70, CH-4056 Basel, Switzerland"
LABEL maintainer.lab="Zavolan Lab"
LABEL maintainer.license="https://spdx.org/licenses/Apache-2.0"

##### VARIABLES #####
# Use variables for convenient updates/re-usability
ENV SOFTWARE_VERSION 3.6.5_0.15.1

##### INSTALL #####
RUN apt-get update -y \
  && pip install --upgrade pip \
  && pip install pysam==0.15.1 \
  && apt-get autoremove -y && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
