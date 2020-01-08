FROM continuumio/anaconda3
MAINTAINER Pyry-Samuli Lahti

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update
RUN apt-get install -y libgtk2.0-0
RUN conda install -y -c https://conda.anaconda.org/menpo opencv3
RUN conda install -y jupyter

RUN mkdir /opt/notebooks


#/opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser

