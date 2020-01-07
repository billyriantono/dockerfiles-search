FROM python:3.7-slim

RUN apt-get clean \
  && apt-get -y update \
  && apt-get -y install libxtst6 libglib2.0-0 libsm6 libfontconfig1 libxrender1 

RUN pip3 install opencv-python

RUN apt-get -y autoremove
