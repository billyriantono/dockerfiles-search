FROM ubuntu:16.04
MAINTAINER Sarah Nadi, nadi@ualberta.ca


RUN apt-get update 

# Tools necessary for CMPUT 201

RUN apt-get install -y gcc-5
RUN apt-get install -y make
RUN apt-get update
RUN apt-get install -y valgrind
RUN ln -s /usr/bin/gcc-5 /usr/bin/gcc
