#
# Ubuntu Dockerfile
#
# https://github.com/dockerize/ubuntu
#

# Pull base image
FROM ubuntu:14.04

MAINTAINER Dockerize "http://dockerize.github.io"

# Add mirrors
RUN sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list 

# Update OS
RUN apt-get update
RUN apt-get -y upgrade

# Install base packages
RUN apt-get install -y build-essential
RUN apt-get install -y software-properties-common
RUN apt-get install -y zip unzip curl wget vim git man htop

# Add files
ADD .bashrc /root/.bashrc

# Set environment variables
ENV HOME /root

# Define working directory
WORKDIR /root

# Default command
CMD ["bash"]
