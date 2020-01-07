# Go 1.2 Server
#
# VERSION		0.0.1

FROM ubuntu
MAINTAINER Vizidrix <admin@vizidrix.com>

# Update apt-get and it's repositories
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y install wget

# Download and extract the Golang binaries
RUN wget -q http://go.googlecode.com/files/go1.2.linux-amd64.tar.gz
RUN tar -xzf go1.2.linux-amd64.tar.gz

# Setup Golang environment vars
RUN echo "export GOROOT=/go" >> /etc/bash.bashrc
RUN echo "export PATH=$PATH:/go/bin" >> /etc/bash.bashrc

# Cleanup downloaded files
RUN rm go1.2.linux-amd64.tar.gz
