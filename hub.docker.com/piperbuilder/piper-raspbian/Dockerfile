FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y git binutils
RUN apt-get update && apt-get install -y wget zip

WORKDIR /home/piper
ENV RASPBIAN_LATEST raspbian-2018-06-29/2018-06-27-raspbian-stretch.zip
RUN wget -O raspbian_latest https://downloads.raspberrypi.org/raspbian/images/$RASPBIAN_LATEST

CMD ls
