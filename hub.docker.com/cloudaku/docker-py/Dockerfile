from phusion/baseimage:latest
maintainer AnyBucket Project "http://www.anybucket.org"
RUN apt-get update
RUN yes | apt-get install python-pip
ADD . /home/docker-py
RUN cd /home/docker-py && pip install .
