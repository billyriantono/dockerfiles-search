# Base image from Ubuntu #
FROM ubuntu:17.10

LABEL base.image="ubuntu:17.10"
LABEL software="STAR, hisat2"
LABEL software.version="2.5.3a, 2.1.0"
LABEL maintainer="Mike Smith <msmith@bioneos.com>"

USER root

# Prep our container
RUN apt-get update && apt-get install curl unzip python gcc make libncurses5-dev zlib1g-dev libbz2-dev liblzma-dev -y

# Add samtools
RUN curl -sL https://github.com/samtools/samtools/releases/download/1.8/samtools-1.8.tar.bz2 | tar xj -C /tmp/
WORKDIR /tmp/samtools-1.8/
RUN ./configure
RUN make && make install

# Add STAR v 2.5.3a, placed in /opt (using the static binary)
RUN curl -sL https://github.com/alexdobin/STAR/archive/2.5.3a.tar.gz | tar xz -C /opt/

# Add HISAT2 v 2.1.0
WORKDIR /tmp
RUN curl -sL ftp://ftp.ccb.jhu.edu/pub/infphilo/hisat2/downloads/hisat2-2.1.0-Linux_x86_64.zip -o hisat2-2.1.0.zip && \
  unzip -d /opt/ hisat2-2.1.0 && \
  rm hisat2-2.1.0.zip

# Add our tools to the PATH
ENV PATH /opt/STAR-2.5.3a/bin/Linux_x86_64_static/:/opt/hisat2-2.1.0/:$PATH

# Default command
CMD /bin/bash
