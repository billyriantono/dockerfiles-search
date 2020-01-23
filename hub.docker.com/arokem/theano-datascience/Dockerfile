FROM wiseio/datascience-base

# make sure the package repository is up to date
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" >> /etc/apt/sources.list
RUN apt-get update

# install basic
RUN apt-get install -y build-essential gfortran g++ libopenblas-dev git

# install Theano (development version)
RUN cd /opt && git clone git://github.com/Theano/Theano.git
RUN cd /opt/Theano && python setup.py develop
