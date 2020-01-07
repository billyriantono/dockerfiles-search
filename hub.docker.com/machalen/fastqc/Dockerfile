#########################################################################
#RNA-seq Tools
#Dockerfile to use fastqc
#Ubuntu 14.04
##########################################################################

#Build the image based on Ubuntu
FROM ubuntu:14.04

#File Author / Maintainer
MAINTAINER Magdalena Arnal <marnal@imim.es>

#Install OpenJDK 7 JRE
RUN apt-get update && apt-get install --yes openjdk-7-jre perl unzip python

#Download FastQC
ADD http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip /tmp/

#Install FastQC
RUN cd /usr/local && \
  unzip /tmp/fastqc_*.zip && \
  chmod 755 /usr/local/FastQC/fastqc && \
  ln -s /usr/local/FastQC/fastqc && \
  rm -rf /tmp/fastqc_*.zip

#Add FastQC to the path variable
ENV PATH $PATH:/usr/local/FastQC

#Set wokingDir in /
WORKDIR /
