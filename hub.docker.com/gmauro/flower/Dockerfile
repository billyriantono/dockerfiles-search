# Based on Debian-stretch
FROM python:2.7
MAINTAINER Gianmauro Cuccuru <gmauro@gmail.com>

# Install Flower
ENV FLOWER_VERSION='0.9.1'
RUN pip install flower==$FLOWER_VERSION 

EXPOSE 5555

# Run Flower
ENTRYPOINT ["flower", "--port=5555"]

