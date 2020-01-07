FROM ubuntu:14.04
MAINTAINER Paul English "paul@onfrst.com"
RUN apt-get -qq update && apt-get upgrade -y
RUN apt-get install -y \
    python-dev \
    python-setuptools \
    supervisor \
    git-core \
    make \
    python-numpy
RUN easy_install pip
RUN pip install virtualenv
RUN pip install uwsgi
EXPOSE 8000
