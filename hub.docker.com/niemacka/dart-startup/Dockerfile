FROM debian:latest

RUN apt-get update 

RUN DEBIAN_FRONTEND=noninteractive apt-get -y upgrade

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
  git \ 
  libnetcdff-dev \
  libnetcdf-dev \
  netcdf-bin \
  gfortran \
  csh \
  make
