FROM rocker/r-parallel

MAINTAINER "Stuart Russell" stuartrussell@nantwichfarmvets.co.uk

RUN echo "deb http://deb.debian.org/debian bullseye main" > /etc/apt/sources.list

# Configure the build environment per
# https://github.com/stan-dev/rstan/wiki/Installing-RStan-on-Mac-or-Linux
RUN mkdir $HOME/.R \
  && echo "CXX14FLAGS=-O3 -march=native -mtune=native -fPIC" > $HOME/.R/Makevars \
  && echo "CXX14=g++" >> $HOME/.R/Makevars
ENV MAKEFLAGS "-j4"

# Install rstan dependencies
RUN install2.r RcppEigen

#RUN install2.r rstan
RUN apt-get update && apt-get install -y r-cran-rstan

