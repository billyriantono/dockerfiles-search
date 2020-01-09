FROM ubuntu:18.04
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install --yes  \
  build-essential \
  apt-utils \
  git-all \
  perl \
  unzip \
  wget \
  openjdk-8-jdk 
  
WORKDIR /opt
#RUN curl -s https://get.nextflow.io | bash
RUN wget -qO- https://get.nextflow.io | bash
RUN cp /opt/nextflow /usr/local/bin
