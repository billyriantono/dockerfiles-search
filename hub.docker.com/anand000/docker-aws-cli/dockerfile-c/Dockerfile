FROM ubuntu:16.04

MAINTAINER amutake <amutake.s@gmail.com>

RUN apt-get update -qq -y
RUN apt-get install -qq -y pdftk imagemagick libimage-exiftool-perl xpdf

RUN mkdir /workdir
WORKDIR /workdir
