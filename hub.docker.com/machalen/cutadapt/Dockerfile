#########################################################
# Dockerfile to build Cutadapt container Based on Ubuntu
#########################################################

#Set the image based on Ubuntu
FROM ubuntu:14.04

#File Author/Maintainer
MAINTAINER Magdalena Arnal, marnal@imim.es

#Update the repository sources list and install essential libraries
RUN apt-get update && apt-get install --yes build-essential

#Install pip and cutadapt required libraries
RUN apt-get install --yes python-pip libpython2.7-dev

#Install cutadapt
RUN pip install cutadapt

#Set wokingDir in /
WORKDIR /
