FROM continuumio/miniconda3:latest
LABEL maintainer="a.kuederle@gmail.com"

# Install openjdk8
RUN apt-get update && apt-get install -y openjdk-8-jdk
    
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

# Update conda and pip
RUN conda update -n base conda
RUN pip install pip --upgrade

# Install Cython and virtualenv, that sometimes produce issues when installed later
RUN apt-get update --fix-missing && apt-get install -y gcc
RUN python -m pip install --upgrade Cython
RUN conda install virtualenv -y

# Install build-essentials for make
RUN apt-get install build-essential -y

