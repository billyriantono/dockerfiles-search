FROM ubuntu:16.04

# Author
MAINTAINER dangminhtruong


RUN apt-get update && apt-get -y upgrade

# Install curl
RUN apt-get -y install curl

# Down load golang

RUN curl -O https://storage.googleapis.com/golang/go1.9.1.linux-amd64.tar.gz
RUN tar -xvf go1.9.1.linux-amd64.tar.gz
RUN mv go /usr/local

# Setting Go Paths
RUN echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.bashrc
RUN echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.profile
RUN . ~/.bashrc

# Create working folder
RUN mkdir $HOME/work
RUN export GOPATH=$HOME/work

WORKDIR $HOME/work
