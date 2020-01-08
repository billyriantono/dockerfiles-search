############################################################
# Dockerfile: Build environment for latex document builds  #
# Based on Ubuntu                                          #
############################################################

# Set the base image to Ubuntu
FROM ubuntu:xenial

# File Author / Maintainer
MAINTAINER Viktor Richter

# Update the repository sources list
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y

# Install dependencies
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y inkscape make wget graphviz curl default-jdk-headless python-pygments
RUN apt-get clean

ADD texlive.profile /opt/install-tl/

# Get Texlive installer
RUN mkdir -p opt/install-tl &&\
   cd opt/install-tl &&\
   wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz &&\
   tar -xzf install-tl-unx.tar.gz &&\
   mv */* . && \
   ./install-tl -profile texlive.profile &&\
   rm -rf /opt/install-tl

# Set environment
ENV USER ci
ENV PATH="/usr/local/texlive/2018/bin/x86_64-linux:${PATH}"
