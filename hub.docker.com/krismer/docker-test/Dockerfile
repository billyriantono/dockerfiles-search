FROM ubuntu:16.04

MAINTAINER Konstantin Krismer <krismer@mit.edu>

RUN apt-get update
RUN apt-get -q -y install python-pip man parallel

RUN pip install numpy h5py torch --no-cache-dir

RUN mkdir /scripts
ADD * /scripts/
WORKDIR /scripts