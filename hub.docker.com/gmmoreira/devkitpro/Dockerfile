FROM ubuntu:16.04

RUN apt-get update && \
  apt-get install -y \
  git \
  curl \
  imagemagick \
  wget \
  bzip2 \
  make \
  vim-common \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /root

RUN curl -L http://sourceforge.net/projects/devkitpro/files/Automated%20Installer/devkitARMupdate.pl/download -o devkitARMupdate.pl
RUN chmod +x ./devkitARMupdate.pl
RUN ./devkitARMupdate.pl /opt/devkitpro
RUN rm -f *.bz2
RUN rm -f *.pl
ENV DEVKITPRO /opt/devkitpro
ENV DEVKITARM $DEVKITPRO/devkitARM
ENV PATH $PATH:$DEVKITARM/bin
