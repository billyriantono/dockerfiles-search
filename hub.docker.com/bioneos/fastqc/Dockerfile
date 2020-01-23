# Base image from Ubuntu #
FROM ubuntu:17.10

LABEL base.image="ubuntu:17.10"
LABEL software="FastQC"
LABEL software.version="0.11.5"
LABEL maintainer="Mike Smith <msmith@bioneos.com>"

USER root

# Prep our container
RUN apt-get update && apt-get install curl unzip default-jre libfindbin-libs-perl -y

# Add gffread v 0.9.9, placed in /opt (using the static binary) and cleanup our directory structure
RUN mkdir /opt/fastqc-0.11.5 && \
  curl -sL https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip -o /tmp/fastqc-0.11.5.zip && \ 
  unzip -d /opt/fastqc-0.11.5 /tmp/fastqc-0.11.5.zip && \
  mv /opt/fastqc-0.11.5/FastQC/* /opt/fastqc-0.11.5 && \
  rm -rf /tmp/fastqc-0.11.5.zip /opt/fastqc-0.11.5/FastQC

# Set permissions to execute fastqc
RUN chmod a+x /opt/fastqc-0.11.5/fastqc

# Add our tool to the PATH
ENV PATH /opt/fastqc-0.11.5/:$PATH

# Default command
CMD /bin/bash
