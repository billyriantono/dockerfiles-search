FROM ubuntu:16.04
MAINTAINER Marcin Baszczewski <marcin@baszczewski.pl>

# set locale
RUN locale-gen pl_PL.UTF-8  
ENV LANG pl_PL.UTF-8  
ENV LANGUAGE pl_PL:pl  
ENV LC_ALL pl_PL.UTF-8

# set timezone
RUN echo Europe/Warsaw >/etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

# update system
RUN DEBIAN_FRONTEND=noninteractive apt-get update -yq
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -yq

# setup packages
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq sudo mc wget net-tools iputils-ping apt-utils