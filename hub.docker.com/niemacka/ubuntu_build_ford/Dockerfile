FROM ubuntu:18.04

RUN apt-get update && apt-get -y upgrade && \
    apt-get -y install python-pip \
                       git \
                       openssh-server \
                       graphviz \
                       findutils \
                       gfortran && \
                       pip install ford
