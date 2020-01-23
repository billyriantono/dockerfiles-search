FROM phusion/baseimage:0.9.18

RUN apt-get update && \
  apt-get install -y python python-pip && \
  apt-get clean all -y

RUN pip install luigi
