# Python 3.7 | Django
FROM python:3

MAINTAINER Gonzalo Fernandez [gonzalo@nuvoltic.com]
####################################################
# Environment variables
####################################################
ENV PYTHONUNBUFFERED 1
####################################################
# OS Updates and Python packages
####################################################
RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y
RUN apt-get install -y apt-utils
####################################################
# A Few pip installs not commonly in requirements.txt
####################################################
RUN apt-get install -y nano wget gettext
# build dependencies for image bindings
RUN apt-get install -y python-imaging
####################################################
# Install dependencies and run scripts.
####################################################
RUN mkdir /code/
WORKDIR /code/
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ADD . /code/
# Expose listen ports
EXPOSE 80
