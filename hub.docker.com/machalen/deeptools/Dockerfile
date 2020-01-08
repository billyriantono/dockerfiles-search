#########################################################
# Dockerfile to build deeptools image Based on Ubuntu
#########################################################

#Set the image based on Ubuntu
FROM ubuntu:latest

#File Author/Maintainer
MAINTAINER Magdalena Arnal, marnal@imim.es

#Update the repository sources list and install essential libraries
RUN apt-get update && apt-get install --yes build-essential

#Install pip and deeptools required libraries
RUN apt-get install --yes python-pip libpython2.7-dev zlib1g-dev libbz2-dev liblzma-dev

#Install requirements
RUN pip install numpy scipy py2bit pyBigWig pysam matplotlib

#Install deeptools
RUN pip install deeptools

#Set wokingDir in /
WORKDIR /
