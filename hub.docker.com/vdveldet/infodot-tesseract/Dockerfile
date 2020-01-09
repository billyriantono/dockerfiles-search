FROM ubuntu:16.04
ENV DEBIAN_FRONTEND noninteractive

MAINTAINER vdvelde.t@gmail.com

RUN apt-get update && apt-get install -y software-properties-common && add-apt-repository -y ppa:alex-p/tesseract-ocr
RUN apt-get update && apt-get install -y tesseract-ocr tesseract-ocr-nld imagemagick

RUN mkdir /home/work
WORKDIR /home/work
