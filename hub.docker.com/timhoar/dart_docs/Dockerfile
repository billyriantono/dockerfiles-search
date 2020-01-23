FROM ubuntu:18.04

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y install python-pip \
                       pandoc \
                       git \
                       vim \
                       openssh-server \
                       graphviz \
                       findutils \
                       gfortran && \
    pip install ford
