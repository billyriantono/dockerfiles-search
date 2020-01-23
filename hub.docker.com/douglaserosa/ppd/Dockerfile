FROM ubuntu:18.04
LABEL maintainer="Douglas Eduardo Rosa douglas.erosa@gmail.com"

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y make
RUN apt-get install -y gcc
RUN apt-get install -y g++
RUN apt-get install -y gfortran
RUN apt-get install -y mpich
RUN apt-get install -y vim

RUN apt-get autoremove
RUN apt-get clean
