# Create the OS container
FROM ubuntu:rolling

LABEL maintainer="RavenX8"

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive \
  apt-get -q -y install g++-8 cmake git curl libcurl4-gnutls-dev wget unzip autoconf libtool libssl-dev python python-pip perl mysql-client libmysqlclient-dev libncurses5-dev libreadline-dev \
  && apt-get clean

RUN pip install --user pyparsing

WORKDIR /usr
RUN git clone https://github.com/ninja-build/ninja.git /usr/ninja && cd ninja && \
    git checkout release && \
	  ./configure.py --bootstrap && \
	  cd ..
	  
ENV PATH="/usr/ninja:${PATH}"
