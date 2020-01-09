##### BASE IMAGE #####

FROM continuumio/miniconda:4.5.12

##### METADATA #####
LABEL base.image="continuumio/miniconda:4.5.12"
LABEL version="1"
LABEL software="rmats2sashimiplot"
LABEL software.version="2.0.3"
LABEL software.description="rmats output to sashimi plots"
LABEL software.website="https://github.com/Xinglab/rmats2sashimiplot"
LABEL software.documentation="https://github.com/Xinglab/rmats2sashimiplot"
LABEL software.license="https://github.com/Xinglab/rmats2sashimiplot/blob/master/LICENSE"
LABEL software.tags="Genomics,Transcriptomics"
LABEL maintainer="foivos.gypas@unibas.ch"
LABEL maintainer.organisation="Biozentrum, University of Basel"
LABEL maintainer.location="Klingelbergstrasse 50/70, CH-4056 Basel, Switzerland"
LABEL maintainer.lab="Zavolan Lab"
LABEL maintainer.license="https://spdx.org/licenses/Apache-2.0"

##### VARIABLES #####
ENV SOFTWARE_VERSION 2.0.3

##### INSTALL #####
RUN apt-get update -y \
  && conda install -c bioconda rmats2sashimiplot=${SOFTWARE_VERSION}
