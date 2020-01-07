FROM debian:wheezy

MAINTAINER Matthias Georgi <matti.georgi@gmail.com>

RUN apt-get update
RUN apt-get install -y curl bzip2
RUN curl http://repo.continuum.io/miniconda/Miniconda-3.7.0-Linux-x86_64.sh > anaconda.sh
RUN chmod +x anaconda.sh
RUN ./anaconda.sh -b -panaconda
RUN ./anaconda/bin/conda install --yes pip psycopg2

