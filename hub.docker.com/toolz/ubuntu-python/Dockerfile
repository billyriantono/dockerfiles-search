# build: docker build -t toolz/ubuntu-python .
#
# run: docker run -d toolz/ubuntu-python
#
# debug: docker run -i -t toolz/ubuntu-python /bin/bash
#
# develop: docker run -p 8080:80 -d -v myapp.py:/root/myapp.py

FROM ubuntu:16.04

MAINTAINER Maurice de Vries

ENV TERM xterm

RUN apt-get update
#RUN apt-get -y upgrade
RUN apt-get -y install python

# Copy app into place.
#ADD myscript.py /root/myapp.py	

