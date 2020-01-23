FROM node:6.9.4

MAINTAINER Igor Malyk "malyk.igor@gmail.com"

RUN \
  apt-get update && \
  apt-get install -y \
  build-essential \
  libxml2-dev \
  libxslt1-dev \
  software-properties-common \
  python-software-properties \
  python g++ make zsh curl wget git unzip vim telnet htop

RUN npm install -g bower grunt-cli gulp webpack karma http-server

CMD bash
