FROM ubuntu:16.04

SHELL ["/bin/bash", "-c"]

# Set locale
RUN apt-get update && apt-get install -y locales && locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

RUN apt-get update && \
    apt-get install -y wget software-properties-common && \
    add-apt-repository ppa:ubuntugis/ubuntugis-unstable && \
    apt-get update && \
    apt-get install -y grass grass-dev python python-pip && \
    pip install biopython geojson ete2 pyshp && \
    pip install pandas==0.19.2 
  
