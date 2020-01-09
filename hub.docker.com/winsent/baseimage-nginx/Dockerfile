FROM ubuntu:14.04

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
RUN echo "deb http://nginx.org/packages/mainline/ubuntu/ trusty nginx" >> /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
  supervisor \
  nginx \
  curl \
  mercurial \
  git \
  python-dev \
  python-virtualenv \
  libgdal-dev \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
  