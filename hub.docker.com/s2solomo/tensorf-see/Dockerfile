FROM tensorflow/tensorflow:latest-gpu

MAINTAINER Shashank Solomon <s2solomo@ucsd.edu>

# Upgrade pip
RUN pip install --upgrade pip

# update stuff
RUN apt-get update

# Install useful python libraries and tools
RUN apt-get install -y vim
RUN pip install keras
