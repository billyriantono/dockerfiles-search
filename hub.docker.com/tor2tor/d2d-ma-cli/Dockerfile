FROM ubuntu:16.04
ENV LANG C.UTF-8

RUN apt-get update -y
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections
RUN apt-get install -y software-properties-common python3-software-properties
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test
RUN add-apt-repository -y ppa:ubuntugis/ubuntugis-unstable
RUN add-apt-repository -y ppa:jonathonf/python-3.6
RUN apt-get update -y
RUN apt-get install -y g++-5
RUN apt-get -y install build-essential
RUN apt-get -y install curl
RUN apt-get -y install libspatialindex-dev
RUN apt-get -y install libsqlite3-dev
RUN apt-get -y install gcc gfortran libblas-dev liblapack-dev cython
RUN apt-get -y install zlib1g-dev
RUN apt-get -y install gdal-bin
RUN apt-get -y install libgdal-dev
RUN apt-get -y install python3.6
RUN apt-get -y install python3.6-dev
RUN apt-get -y install git
RUN apt-get -y install netcat-traditional
RUN apt-get -y install postgresql-client

RUN rm /usr/bin/python
RUN ln -s /usr/bin/python3.6 /usr/bin/python
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py

RUN export CXX=g++-5
RUN curl -L https://github.com/mapbox/tippecanoe/archive/1.32.5.tar.gz | tar zx
WORKDIR /tippecanoe-1.32.5
RUN make
RUN make install

COPY requirements.txt /opt/app/requirements.txt
COPY dev_requirements.txt /opt/app/dev_requirements.txt
COPY Makefile /opt/app/Makefile
WORKDIR /opt/app
RUN make install
