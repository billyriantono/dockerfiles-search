FROM php:cli

MAINTAINER Randy Hommel

RUN apt-get update && apt-get install -y python-pip
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install awscli
