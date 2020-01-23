from ubuntu:latest

LABEL maintainer="anders.savill@csiro.au"

#This container installs pre-requisits for 2DFDR and compiles it

#Let's start by updating the system and installing the required software
RUN apt-get update \
      && apt-get install -y autoconf automake gcc g++ make gfortran wget python python-dev libx11-dev \
      && apt-get clean all \
      && rm -rf /var/lib/apt/lists/*

#Make a temp work directory
RUN mkdir /tmp/2dfdr-build
WORKDIR /tmp/2dfdr-build

#Download 2DFDR Source, configure, compile, clean up
RUN wget ftp://anonymous@ftp.aao.gov.au/pub/local/2dfdr/releases/6.46/2dfdr-6.46.tar.gz \
      && tar xvzf 2dfdr-6.46.tar.gz \
      && cd 2dfdr-6.46 \
      && ./configure --help \
      && ./configure --disable-x \
      && make \
      && make install \
      && cd / \
      && rm -rf /tmp/2dfdr-build

#Sent environment variable
ENV PATH /usr/local/2dFdr/bin:${PATH}
RUN echo $PATH
CMD ["/bin/bash"]
