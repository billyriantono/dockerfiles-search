# This is custom image to be use in CircleCI environment.
# It customizes base Python image by installing libraries required by GeoDjango.
# Repository name is cleolabs/python:<tag> e.g. cleolabs/python:3.7.1
#

FROM python:3.7.1

# System prerequisites
RUN apt-get update \
 && apt-get -y upgrade \
 && apt-get -y install build-essential libpq-dev binutils libproj-dev gdal-bin \
 && rm -rf /var/lib/apt/lists/*

RUN apt-get -y --purge remove mercurial && apt-get -y autoremove
RUN apt-get -y --purge remove imagemagick && apt-get -y autoremove
# RUN apt-get -y --purge remove mariadb-server && apt-get -y autoremove
