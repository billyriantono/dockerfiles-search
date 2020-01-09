FROM ubuntu:18.04
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y mercurial gosu python-dev python-setuptools python-gdal python-rtree python-shapely python-matplotlib python-qt4 libgdal-dev python-pip libfreetype6-dev gfortran
RUN pip install Cython
RUN pip install hg+https://bitbucket.org/natcap/invest/@3.6.0 qtpy>1.3 qtawesome faulthandler
ENV DEBIAN_FRONTEND teletype
ENTRYPOINT gosu $USERNAME bash -c '/usr/local/bin/invest launcher'
